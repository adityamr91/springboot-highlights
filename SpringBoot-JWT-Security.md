
1. Hit /authenticate rest end using username & password in app.properties
2. Service class will take the call from controller class and validate username & password and then geneates JWTtoken with a timestamp from the help of JWT tokenUtil.java
3. next time when we hit any rest ends is it it should be with the JwtToken in the header of the http request
4. now the AutheticationEntry point intercepts the request and validtaes the JwtToken and its timestamp with the help of JWtRequestFilter
5. once everything is ok in the above steps WebConfig does the authorization and maintains the degree of levels of access of rest end points

**Controller Class with Authetication Process RestEnd Point**
```
@RestController
@CrossOrigin
public class JwtAuthenticationController {

	@Autowired
	private AuthenticationManager authenticationManager;

	@Autowired
	private JwtTokenUtil jwtTokenUtil;

	@Autowired
	private UserDetailsService jwtInMemoryUserDetailsService;

//	@RequestMapping(value = "/authenticate", method = RequestMethod.POST)
//	public ResponseEntity<?> createAuthenticationToken(@RequestBody JwtRequest authenticationRequest)
	@RequestMapping(value = "/rest/authenticate")
	public ResponseEntity<?> createAuthenticationToken()
			throws Exception {

//		authenticate(authenticationRequest.getUsername(), authenticationRequest.getPassword());
		authenticate("javainuse", "password");
		final UserDetails userDetails = jwtInMemoryUserDetailsService
				.loadUserByUsername("javainuse");

		final String token = jwtTokenUtil.generateToken(userDetails);
//		jwtTokenUtil.setToken(token);
		return ResponseEntity.ok(new JwtResponse(token));
	}

	private void authenticate(String username, String password) throws Exception {
		Objects.requireNonNull(username);
		Objects.requireNonNull(password);

		try {
			authenticationManager.authenticate(new UsernamePasswordAuthenticationToken(username, password));
		} catch (DisabledException e) {
			throw new Exception("USER_DISABLED", e);
		} catch (BadCredentialsException e) {
			throw new Exception("INVALID_CREDENTIALS", e);
		}
	}
}
```
**Service Class to Pass Username and Password* for Authentication*
```
@Primary
@Service
public class JwtUserDetailsService implements UserDetailsService {

	@Override
	public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
		if ("javainuse".equals(username)) {
			return new User("javainuse", "$2a$10$slYQmyNdGzTn7ZLBXBChFOC9f6kFjAqPhccnP6DxlWXx2lPk1C3G6",
					new ArrayList<>());
		} else {
			throw new UsernameNotFoundException("User not found with username: " + username);
		}
	}

}
```

**Authetication Entry Point**
```
@Component
public class JwtAuthenticationEntryPoint implements AuthenticationEntryPoint, Serializable {

	private static final long serialVersionUID = -7858869558953243875L;

	@Override
	public void commence(HttpServletRequest request, HttpServletResponse response,
			AuthenticationException authException) throws IOException {

		response.sendError(HttpServletResponse.SC_UNAUTHORIZED, "Unauthorized");
	}
}
```
**Websecurity Config / Gateway of Accessing all restend points**
```
@Configuration
@EnableWebSecurity
@EnableGlobalMethodSecurity(prePostEnabled = true)
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

	@Override
	protected void configure(HttpSecurity httpSecurity) throws Exception {
		// We don't need CSRF for this example
		httpSecurity.csrf().disable()
				// dont authenticate this particular request
				.authorizeRequests().antMatchers("/rest/authenticate", "/**/rest/authenticate", "/**/rest/safe/**", "/assets/**", "/*", "/**/rest/generic/getEnvironment", 
						"/**/rest//user/updateTimeZone", "/**/rest/user/active/**", "/**/rest//file/checkUserImageExist**")
				.permitAll().
				// all other requests need to be authenticated
				anyRequest().authenticated().and().
				// make sure we use stateless session; session won't be used to
				// store user's state.
				exceptionHandling().authenticationEntryPoint(jwtAuthenticationEntryPoint).and().sessionManagement()
				.sessionCreationPolicy(SessionCreationPolicy.STATELESS);

		// Add a filter to validate the tokens with every request
		httpSecurity.addFilterBefore(jwtRequestFilter, UsernamePasswordAuthenticationFilter.class);
	}
}
```

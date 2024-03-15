### How do you admin and client roles with spring.security.oauth2?


To administer and assign roles such as `ADMIN` and `CLIENT` to users in a Spring Security OAuth2 application, you can follow these steps, combining insights from the provided sources:

1. Define Roles in Your Application: First, ensure you have defined the roles (`ADMIN`, `CLIENT`, etc.) in your application. These roles are typically represented as `GrantedAuthority` objects in Spring Security.

2. Customize User Authorities: When a user logs in using OAuth2, you might want to map the roles from your database to the authorities in Spring Security. This can be achieved by customizing the `OAuth2UserService` or using a `GrantedAuthoritiesMapper`. The `GrantedAuthoritiesMapper` allows you to transform the authorities granted to the user by the OAuth2 provider into the authorities your application uses.

```java
@Bean
public GrantedAuthoritiesMapper userAuthoritiesMapper() {
    return (authorities) -> {
        Set<GrantedAuthority> mappedAuthorities = new HashSet<>();
        authorities.forEach(authority -> {
            // Map the authority to your application's roles
            // For example, if the OAuth2 provider grants a "ROLE_ADMIN" authority,
            // you might want to map it to your application's "ADMIN" role
            if ("ROLE_ADMIN".equals(authority.getAuthority())) {
            mappedAuthorities.add(new SimpleGrantedAuthority("ADMIN"));
            }
            // Add other mappings as needed
        });
        return mappedAuthorities;
    };
}
```

3. Configure Security to Use Custom Authorities Mapper: In your security configuration, ensure that the `OAuth2UserService` or `GrantedAuthoritiesMapper` you've defined is used. This can be done by configuring the `OAuth2LoginConfigurer` in your `HttpSecurity` configuration.

```java
@Override
protected void configure(HttpSecurity http) throws Exception {
    http
        .oauth2Login()
            .userInfoEndpoint()
                .userService(customOAuth2UserService())
                .and()
            .authorizedClientService(authorizedClientService())
            .authorizedClientRepository(authorizedClientRepository())
            .and()
        .authorizeRequests()
            .antMatchers("/admin/**").hasRole("ADMIN")
            .antMatchers("/client/**").hasRole("CLIENT")
            .anyRequest().authenticated();
}
```

4. Use Roles in Security Constraints: When configuring security constraints, use the roles you've defined. For example, to restrict access to certain endpoints to users with the `ADMIN` role, you can use `.hasRole("ADMIN")`.

```java
http
    .authorizeRequests()
    .antMatchers("/admin/**").hasRole("ADMIN")
    .antMatchers("/client/**").hasRole("CLIENT")
    .anyRequest().authenticated();
```
5. Database Integration: Ensure your application's database is integrated with Spring Security to manage user roles. This typically involves storing user roles in your database and querying them when a user logs in to map them to the authorities in Spring Security.

By following these steps, you can effectively administer and assign roles such as `ADMIN` and `CLIENT` to users in your Spring Security OAuth2 application, ensuring that users have the appropriate permissions based on their roles 135.
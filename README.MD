# Management of refresh tokens

Go to System Settings - Module Container - Component Blacklist
Add `com.liferay.portal.security.sso.openid.connect.internal.OpenIdConnectServiceHandlerImpl` to the black list

In a configuration where Refresh tokens have a short lifespan, you'd rather have a short session time and session auto
extend so that we have a guarantee that frequent requests are sent to Liferay so as to trigger the servlet filter
that is responsible for the renewal of OIDC tokens.

Session timeout should be less than the half lifespan of the OIDC ID Token because we provide that time window
for anticipated token refresh.

portal-ext.properties
```
    session.timeout=5
    session.timeout.warning=1
    session.timeout.auto.extend=false
    session.timeout.auto.extend.offset=30
```

# secure_headers
Headers for nginx, axis etc.

Service for testing: https://webbkoll.dataskydd.net/

Paste into nginx.conf

```
    add_header Strict-Transport-Security "max-age=31536000; includeSubdomains; preload";
    add_header X-XSS-Protection "1; mode=block";
    add_header Content-Security-Policy "frame-ancestors 'self'; default-src 'none'; base-uri 'self'; form-action 'self'; script-src 'self'';" always;
    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-Content-Type-Options nosniff;
```
Headers for axios
```
const checkUrlAndSetSecureHeaders = !/http(s)?:\/\/localhost/.test(config.currentAddress)
  ? {
    'Strict-Transport-Security': 'max-age=31536000; includeSubdomains; preload',
    'Content-Security-Policy': `frame-ancestors 'self'; default-src 'none'; base-uri 'self'; form-action 'self'; script-src 'self'; img-src 'self'; object-src 'none'; style-src 'self'; connect-src 'self'; font-src 'self'; media-src 'self'; frame-src 'self'; child-src 'self';`,
    'X-XSS-Protection': '1',
    'X-Frame-Options': 'SAMEORIGIN',
    'X-Content-Type-Options': 'nosniff',
    'Referrer-Policy': 'no-referrer'
  }
  : {};
  
const getDefaultHeaders = () => ({
  // eslint-disable-next-line object-curly-newline
  Authorization: `Bearer ${Storage.getToken()}`,
  standalone: navigator.standalone || (window.matchMedia('(display-mode: standalone)').matches),
  ...checkUrlAndSetSecureHeaders
});

```

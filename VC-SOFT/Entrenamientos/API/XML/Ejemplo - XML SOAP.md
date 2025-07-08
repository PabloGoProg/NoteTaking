- Contexto - Operación de Login
### Petición
``` XML
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
                  xmlns:aut="http://auth.empresa.com/LoginService"
                  xmlns:wsse="http://schemas.xmlsoap.org/ws/2002/07/secext">

  <soapenv:Header>
    <wsse:Security>
	  -- Credenciales del cliente
      <wsse:UsernameToken>
        <wsse:Username>admin_app</wsse:Username>
        <wsse:Password>supersecreto123</wsse:Password>
      </wsse:UsernameToken>
    </wsse:Security>
  </soapenv:Header>

  <soapenv:Body>
    <aut:loginUsuario>
	  -- Credenciales del usuario
      <aut:usuario>jlopez</aut:usuario>
      <aut:clave>claveSegura456</aut:clave>
    </aut:loginUsuario>
  </soapenv:Body>
</soapenv:Envelope>
```

### Respuesta - Exitosa
```XML
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
                  xmlns:aut="http://auth.empresa.com/LoginService">

  <soapenv:Body>
    <aut:loginUsuarioResponse>
      <aut:resultadoAutenticacion>true</aut:resultadoAutenticacion>
      <aut:idUsuario>7843</aut:idUsuario>
      <aut:rol>Administrador</aut:rol>
      <aut:tokenSesion>eyJhbGciOiJIUzI1NiIsInR...</aut:tokenSesion>
    </aut:loginUsuarioResponse>
  </soapenv:Body>
</soapenv:Envelope>
```

### Respuesta - Error
```XML
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
  <soapenv:Body>
    <soapenv:Fault>
      <faultcode>soapenv:Client</faultcode>
      <faultstring>Credenciales inválidas: usuario o contraseña incorrectos</faultstring>
      <faultactor>http://auth.empresa.com/LoginService</faultactor>
      <detail>
        <error xmlns="http://auth.empresa.com/LoginService">
          <codigo>401</codigo>
          <mensaje>El usuario 'jlopez' no pudo ser autenticado</mensaje>
        </error>
      </detail>
    </soapenv:Fault>
  </soapenv:Body>
</soapenv:Envelope>
```
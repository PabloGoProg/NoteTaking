- Contexto - Servicio de Autenticación

```XML
<?xml version="1.0" encoding="UTF-8"?>
<definitions xmlns="http://schemas.xmlsoap.org/wsdl/"
             xmlns:tns="http://auth.empresa.com/LoginService"
             xmlns:xsd="http://www.w3.org/2001/XMLSchema"
             xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/"
             targetNamespace="http://auth.empresa.com/LoginService"
             name="LoginService">

  <!-- Tipos de datos -->
  <types>
    <xsd:schema targetNamespace="http://auth.empresa.com/LoginService">

      <!-- Entrada del login -->
      <xsd:element name="loginUsuarioRequest">
        <xsd:complexType>
          <xsd:sequence>
            <xsd:element name="usuario" type="xsd:string"/>
            <xsd:element name="clave" type="xsd:string"/>
          </xsd:sequence>
        </xsd:complexType>
      </xsd:element>

      <!-- Respuesta del login -->
      <xsd:element name="loginUsuarioResponse">
        <xsd:complexType>
          <xsd:sequence>
            <xsd:element name="resultadoAutenticacion" type="xsd:boolean"/>
            <xsd:element name="idUsuario" type="xsd:int" minOccurs="0"/>
            <xsd:element name="rol" type="xsd:string" minOccurs="0"/>
            <xsd:element name="tokenSesion" type="xsd:string" minOccurs="0"/>
          </xsd:sequence>
        </xsd:complexType>
      </xsd:element>

      <!-- Entrada del registro -->
      <xsd:element name="registrarUsuarioRequest">
        <xsd:complexType>
          <xsd:sequence>
            <xsd:element name="usuario" type="xsd:string"/>
            <xsd:element name="clave" type="xsd:string"/>
            <xsd:element name="email" type="xsd:string"/>
            <xsd:element name="rol" type="xsd:string"/>
          </xsd:sequence>
        </xsd:complexType>
      </xsd:element>

      <!-- Respuesta del registro -->
      <xsd:element name="registrarUsuarioResponse">
        <xsd:complexType>
          <xsd:sequence>
            <xsd:element name="exito" type="xsd:boolean"/>
            <xsd:element name="mensaje" type="xsd:string"/>
          </xsd:sequence>
        </xsd:complexType>
      </xsd:element>

    </xsd:schema>
  </types>

  <!-- Mensajes -->
  <message name="LoginUsuarioInput">
    <part name="parameters" element="tns:loginUsuarioRequest"/>
  </message>

  <message name="LoginUsuarioOutput">
    <part name="parameters" element="tns:loginUsuarioResponse"/>
  </message>

  <message name="RegistrarUsuarioInput">
    <part name="parameters" element="tns:registrarUsuarioRequest"/>
  </message>

  <message name="RegistrarUsuarioOutput">
    <part name="parameters" element="tns:registrarUsuarioResponse"/>
  </message>

  <!-- PortType: operaciones disponibles -->
  <portType name="LoginServicePortType">
    <operation name="loginUsuario">
      <input message="tns:LoginUsuarioInput"/>
      <output message="tns:LoginUsuarioOutput"/>
    </operation>
    <operation name="registrarUsuario">
      <input message="tns:RegistrarUsuarioInput"/>
      <output message="tns:RegistrarUsuarioOutput"/>
    </operation>
  </portType>

  <!-- Binding: protocolo y estilo -->
  <binding name="LoginServiceBinding" type="tns:LoginServicePortType">
    <soap:binding transport="http://schemas.xmlsoap.org/soap/http" style="document"/>
    <operation name="loginUsuario">
      <soap:operation soapAction="http://auth.empresa.com/LoginService/loginUsuario"/>
      <input>
        <soap:body use="literal"/>
      </input>
      <output>
        <soap:body use="literal"/>
      </output>
    </operation>
    <operation name="registrarUsuario">
      <soap:operation soapAction="http://auth.empresa.com/LoginService/registrarUsuario"/>
      <input>
        <soap:body use="literal"/>
      </input>
      <output>
        <soap:body use="literal"/>
      </output>
    </operation>
  </binding>

</definitions>
```
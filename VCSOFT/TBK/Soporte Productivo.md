[Documentación DP](https://www.ibm.com/docs/en/datapower-gateway/10.6.0?topic=overview) -> LTS 10.0.8
[Documentación APIC](https://www.ibm.com/docs/en/api-connect/software/10.0.x_cd?topic=api-connect-overview) -> 10.5.0.12 (Usada en TBK)

- Jefe directo - Sebastian Cortes
- Apoyo a: Adrian Bruno (SRE), Hernan Alexis (SRE)

De que cosas (Nosotros no nos responsabilizamos del backend):
- IBM DataPower (API Gateway)
	- Filtrar por IP Origen
	- Filtrar por API key
	- Poner rate limits
	- Hacer monitoreo
	- Funciona como firewall (mas o menos)
	- Cifrado extremo a extremo

**Instancias de DataPower utilizadas en TBK**:
* _DMZ_: Quiere decir desmilitarizada (no se hace nada de transformaciones, está en internet publico expuesto así para que solo filtra por IP, api key, etc.)
- _BBN_: Es el interno que se encarga de transformar datos y hacer cosas realmente, este está protegido detrás de otro F5 balanceador de carga.
### Pasos a Producción

- Debe haber un manual que diga mas o menos que se tiene que cambiar.
- El SRE decide cuando hacerlos (Nosotros de pronto recomendamos, no tenemos autoridad)
- _NUNCA ENVIAR LAS API KEYS (ASI LAS PIDAN)_
- HAY MUY POCAS OCASIONES (A VECES, QUE SE TOCA PONER PADDING CON `=`) en algunas transacciones que rechazan por API KEY así todo esté bien.

Hay ocasiones donde toca agregar IP filters (a traves de la interfaz de files en DataPower) solo con supervision de SRE y con ticket abierto a él.

El Router Inbound es un servicio especifico que es el único que tiene puerto 443 para poder manejar HTTPS y enrutar (se puede ver el enrutamiento en local del servicio en file management) a los diferentes servicios MPG.

_¿Como saber a que servicio pertenece el puerto de router inbound?_ -> HTTP handler buscar puerto.
### Proceso de Trabajo de Arquitectura

1. WAF - Firewall Capa 7
2. F5 WAF - ???
3. DataPower DMZ - Control del enrutamiento desde/hacia internet público
4. F5 GTM - Balanceador de Carga
5. DataPower BBN
6. Backend

### Certificados

En TBK tienen todavía unos viejos que se deben cambiar este año 2026 que es _TRANSBANKCA_, el nuevo es _TBKR_.

Tener mucho cuidado al Issuer (quien emitió el certificado - debería ser el CA), _Not before_ y _not after_ en Validity. y Subject, hacia quien está emitido.
Un certificado puede no ser valido por el S.O no confía en el o por todo lo de arriba.

Algunos servicios tienen asociados certificados y una CA.
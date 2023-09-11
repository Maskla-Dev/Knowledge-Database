# Generalidades
**Guardian Protocol** es un ***liquid staking*** service, el cuál, permite a los usuarios de la red [VARA](https://vara-network.io) invertir el principal activo de cambio de la red (***VARA Tokens***) en los nodos validadores a cambio de un rendimiento. 

Los activos invertidos se contabilizan y distribuyen entre los nodos validadores registrados en Guardian Protocol, potenciando de esta manera su capacidad de participación en la red de VARA. A este mecanismo se le conoce como _staking_.

Dado que el activo es retenido por un periodo fijo, durante ese tiempo el usuario pierde la capacidad de poder utilizar otros servicios, a causa de ello, se idea la creación de otro token (_liquid token_) de proporcionalidad 1:1 con respecto al VARA token, el cuál, sirve como activo colateral. De esta manera, cuando el usuario deposita sus VARA tokens, este mismo recibe tokens líquidos intercambiables proporcionales al valor del VARA token, mitigando de esta manera el congelamiento del mercado de servicios de la red. Se le conoce como _Liquid Staking_ al mecanismo extendido.

![[Guardian_Protocol_architecture.jpeg]]
*Arquitectura del servicio Guardian Protocol*
## Terminología
- ***Pool***: Fondo de inversión de tokens, se caracteriza por tener un periodo de duración, una vez alcanzado, los fondos recolectados son repartidos entre todos los nodos validadores registrados.
- ***gFT***: Gear Fungible Token, cripto-activo principal de la red VARA
- ***gVARA***: Token colateral a *gFT*, equivalencia 1:1.
# Requerimientos
- [ ] El usuario podrá visualizar el balance de *gFT*'s y *gVARA*.
	- [ ] Balance de *gFT* libres
	- [ ] Balance de *gVARA* libres
	- [ ] Balance de *gFT* disponibles para realizar ==stack==
- [ ] El usuario podrá intercambiar VARA por gVARA y viceversa.
- [ ] El usuario podrá realizar ==stack==, ==unstack== y ==withdraw==.
- [ ] El usuario puede registrar su nodo como nodo validador en el servicio.
- [ ] El usuario recibe rendimientos de manera automática.
- [ ] Administrador puede dar soporte de mantenimiento a los diferentes contratos.
	- [ ] Pagar renta
	- [ ] Crear una *Pool*
	- [ ] Detener/Eliminar una *Pool*
# Modelado
El modelado de las diferentes operaciones se basa en el modelo de [actores](https://wiki.gear-tech.io/docs/gear/technology/actor-model), el principio de idempotencia y atomicidad. 

Se identifican 3 operaciones que el usuario puede hacer al utilizar el servicio, siendo stack, unstack y withdraw.

La lógica del servicio requiere de otras operaciones intermedias para completar el ciclo que se describe en la arquitectura del servicio, siendo estas ==register==, ==unregister==, ==share== y ==yield==.
## Stack
El usuario proporciona sus VARA tokens al servicio, encolándolos en una lista de espera para ser repartidos a los validadores, a cambio recibe ***gVARA*** (token colateral). Los VARA estarán disponibles si todavía no se reparten.
### Actores
- **Staker**: Usuario que utiliza el servicio *Guardian Protocol* para depositar VARA tokens.
- **Guardian**: Entidad que procesa las instrucciones del exterior.
- **Custodian**: Entidad de control de los balances del *Staker*. 
- **Backyard**: Entidad proxy de los balances en el proceso de *staking*.
- **Master**: Representa a la entidad que representa al servicio (administrador o master).
- **gFT Contract**: Entidad que se encarga de gestionar *VARA fungible tokens* (estándar ERC-20).
- **gVARA Contract**: Entidad que se encarga de gestionar *gVARA fungible tokens* (estándar ERC-20).
- **Pool**: Entidad que se encarga de gestionar los balances de staking.
## Requisitos
- *Staker* cuenta con una *wallet* válida en la red VARA.
- ~~*Staker* ha aprobado transacciones entre *Staker* y *Empire* con *gFT Contract*~~
- *Staker* ha aprobado transacciones entre *Staker* y *Empire* con *Aerarium*

### Flujo principal
1. El *Staker* envía una solicitud ==stack== a la entidad *Guardian*, especificando la cantidad a depositar, el periodo de staking ~~y la duración del periodo~~.
2. La entidad *Guardian* localiza la instancia de la entidad *Custodian* designada al *Staker*.
3. La entidad *Guardian* reenvía la solicitud ==stack== a la instancia *Custodian*.
4. La entidad *Custodian* envía una solicitud de transferencia de fondos al *gFT Contract*, siendo la entidad *Master* quien recibe y *Staker* quien envía.
5. *gFT Contract* procesa y completa la solicitud
6. *gFT Contract* devuelve a *Custodian* el resultado de la operación.
7. *Custodian* envía una solicitud de transferencia de fondos al *gVARA Contract*, siendo la *Master* quien envía y *Staker* quien recibe.
8. *gVARA Contract* procesa y completa la solicitud.
9. *gVARA Contract* devuelve a *Custodian* el resultado de la operación.
10. *Custodian* actualiza los balances del *Staker*
11. *Custodian* envía una solicitud de ==stack== a la entidad de *Backyard*.
12. *Backyard* recibe la solicitud
13. *Backyard* localiza la instancia *Pool* correspondiente al periodo especificado en la solicitud.
14. *Backyard* envía solicitud ==register== a *Pool*
15. *Pool* procesa la solicitud y actualiza el registro de stakers.
16. *Pool* devuelve mensaje de stack exitoso a *Backyard*.
17. *Backyard* actualiza el estado de registro respecto a los balances globales de las *Pool* existentes.
18. *Backyard* devuelve mensaje de operación exitosa a *Custodian*.
19. *Custodian* actualiza los balances (*gFT* disponibles para ==unstack==).
20. *Custodian* devuelve a *Guardian* mensaje de transacciones exitosas.
21. *Guardian* actualiza sus registros globales.
22. *Guardian* devuelve a *Staker* mensaje de operación exitosa.
23. Fin del flujo.
![[GuardianProtocol_stack_1.drawio.png]]
*Flujo de mensajes*
### Flujos alternativos
#### Gas insuficiente
Durante el intercambio de mensajes entre entidades puede que el gas utilizado para procesar las transacciones no sea suficiente. Cualquiera de estos escenarios debe de ser cubierto reservando gas al procesar cada transacción. 

Debido a ello, es imperativo mantener una estructura idempotente (cada acción estructurarse como Tasks con un ID).
## Unstack
El usuario retira los fondos depositados en la *Pool*. Sólo se elimina
### Actores
### Flujo Principal

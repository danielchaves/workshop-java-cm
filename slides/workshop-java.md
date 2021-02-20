#### DevAcademy 



## Desenvolvendo APIs REST com Java



![Image](imagens/java-json.png)



### Facilitadores:
Note: Essas descrições são parcialmente baseado na realidade...



#### Pablo Monteiro
- Java dev há 200 anos, trocou o chapéu de vaqueiro e a botina pelo teclado e mouse. Hoje é Dev leader na Casa Magalhães e um dos veteranos no time do Varejofacil.



#### Giva
- Programou o portão da caverna de tesouros de Alibabá. A chave criptografada "Abra-te sésamo" é de autoria dele. Atualmente arquiteto do Varejofacil, é também conhecido como "O Oráculo do varejo".



#### Daniel Chaves
- Quando criança, mamãe bateu na cabeça dele e disse: "Esse menino vai ser programador Java". Em 2005 a profecia se concretizou e hoje é arquiteto do Varejofacil.



### Agenda
#### Dia 1
- Conceitos API e REST
- Iniciando com Spring Boot
- Hello API - `/hello`
- Modelos e pesistência
- API CRUD



### Agenda
#### Dia 2
- Validações
- Querying
 - FiQL
 - GraphQL
 - Paginação



### API
- _Application Programming Interface_
- Conjunto de instruções e padrões de programação que servem para *fornecer dados e informações* relevantes de uma determinada aplicação



### REST
- _Representational State Transfer_
- "Padrão" da arquitetura de software para interação de aplicações, usando múltiplos _Web services_.
- _Web resources_
- Textual (JSON, XML, HTML)
- Conjunto de operações (GET, POST, PUT, DELETE, PATCH, CONNECT, OPTIONS, TRACE)



### E RESTful?
- _Client-server_
- _Stateless_
- _Cacheable_
- _Layered system_
- Código sob demanda (opcional)
Note: Seis requisitos definem uma arquitetura RESTful. Cliente-servidor; stateless; cacheability (capacidade de fornecer info para guardar/expirar respostas); suporte a camadas de sistema (proxy, load balancer não deve interferir na comunicação); O servidor pode eventualmente enviar código para o cliente executar...



### Nera 6? Falta um...



#### Interface uniforme
- Identificação de recurso nas requisições (`/pessoas`)
- Manipulação de recursos por suas representações
- Mensagens auto descritivas
- HATEOAS
Note: recursos bem identificados; com a resposta de um get eu consigo fazer um post ou patch; headers (text/json), http status, ajudam a descrever as ações; Hypermedia as the engine of application state - assim como usuario acessando uma pagina as mensagens contem "links" para navegar pelos recursos



```log
GET /pessoas/423
Accept: text/json
```
Note: Recurso (Pessoas)



```log
HTTP 200 - OK
Content-Type: text/json
Content-Length: ...
{
    pessoaId: 423,
    nome: "Fulano de Tal",
    idade: 25,
    links: {
        cnh: "/pessoas/423/cnh"
    }
}
```
Note: Resposta textual (HTML, XML, JSON) e status HTTP. HATEOAS concede links para navegação e se comporta conforme o estado.



#### HTTP _Methods_
- `GET`    - Obter informação do(s) recurso
- `POST`   - Recurso processar a informação contida na requisição
- `PUT`    - Alterar o estado do recurso para o estado contido na requisição
- `DELETE` - Delete né =]
Note: Esses são muito usados



#### HTTP _Methods_
- `PATCH`  - Alterar estado do recurso com requisição parcial
- `HEAD`   - Similar ao `GET` mas não tem _response body_
- `OPTIONS`- Retorna dados de quais outros métodos e operações os servidor suporta
Note: menos usados mas muito útis. Tem mais... TRACE - rastreio de rede, retorna o q enviado / CONNECT - usado pra iniciar comunicação de duas vias com o recurso



#### HTTP _Status_
- 1xx - Resposta informativa
- 2XX - Deu certo, chapa.
- 3XX - Sei não, pergunta ali...
- 4XX - Deu bom não, mas eh contigo...
- 5XX - Deu ruim. Mal minha...
Note: 100 - Continue; 102 - Processando; 200 - OK; 201 - Created; 202 - Accepted; 301 - Moved permanently; 400 - Bad request; 401 - Unauthorized; 404 - Not Found; 500 - Internal server error; 503 - Service unavailable.



#### Teste de Exemplo de código
```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello(@AuthenticationPrincipal Principal principal) {
        return "Hello, " + principal.getName() + "!";
    }

}
```



## Cabou-se
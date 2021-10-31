# Arquitetura comum E-Commerce

A proposta do modelo é descrever o que aconteceria ao acessar a página de um produto de algum e-commerce.

Sabemos que ao acessar a página de produtos de um e-commerce podem acontecer inúmeras coisas, não sendo possível uma reposta sem antes conhecer as restrições do negócio, os requisitos de qualidade, o público alvo, o tipo de e-commerce, entre outras variáveis. No entanto, vamos descrever possíveis cenários, como: eventos, arquitetura, tecnologias, entre outros.

# Diagrama 
Entendimento da arquitetura do e-commerce com diagrama do nível 2, modelo C4 de documentação para arquitetura de software.

![alt text](https://github.com/delesposte/SoftwareArchitecture/blob/main/e-commerce.drawio.png?raw=true)

# Fluxo de dados
1.	O cliente acessa a parte pública do frontend, que poderia ser um site;
2.	O frontend efetua requisições http de recursos estáticos como assets, imagens dos produtos, banners, JavaScript, folhas de estilo, entre outros. de uma CDN, que poderia ser o CloudFront;
3.	A CDN efetua pull de recursos da origem, que poderia ser um S3;
4.	O frontend efetua requisições http de informações do produto para o backend, que poderia ser á página do produto, informações como descrição, preço, entre outros;
5.	O backend recebe as requisições no load balancer, ele distribui o tráfego de entrada em vários destinos na camada de cache. O load balancer poderia ser um Elastic Load Balancing;
6.	Os servidores de cache recebem as requisições e verificam se os dados solicitados existem no cache e se ainda são válidos. Caso sim, retornam os dados. Caso contrário, as requisições são direcionadas para um segundo load balancer. O cache poderia ser EC2 com instâncias da família R, otimizadas para memória e ElastiCache  com banco de dado em memória Redis;
7.	O segundo load balancer distribui o tráfego de entrada em vários destinos na camada de aplicação. O load balancer poderia ser um Elastic Load Balancing;
8.	Os servidores de aplicação recebem as requisições e buscam os dados no banco de dados. A camada de aplicação poderia ser EC2 com instâncias da família C4, otimizadas para computação;
9.	As instâncias dos bancos de dados recebem os comandos, executam e retornam dados. O armazenamento poderia ser RDS com MySQL;

# Consideração
- Caso não esteja visualizando as ligações dos itens e textos do diagrama, pode ser por que eles estão na cor preta e o navegador está com o tema dark.

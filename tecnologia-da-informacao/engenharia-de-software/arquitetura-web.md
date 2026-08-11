PROTOCOLO HTTP / HTTP2

Hypertext Transfer Protocol (HTTP)

Requisição(cliente) -> Resposta(servidor)

HTTP 2

- Multiplexing - requests e respostas paralelos em uma única coneão
- Melhorias de performance

gRPC

RPC: cliente solicita ao servidor um serviço e recebe uma resposta, pode ser síncrono ou assíncrono

gRPC: criado pelo google, utiliza HTTP2, mais performático

protobuffer: tipo de "indexação" de atributos que simplifica a codificação. O gRPC trabalha em cima de um arquivo .proto protobuffer, sabe qual a ação e a mensagem com base nesse arquivo.
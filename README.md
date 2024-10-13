# akita
rinheiro
E aí <galera>, seguinte! 😅😅

Já vi que a galera tá animada pra essa rinha, e eu também tô! 💪💪

Mas como um bom Akita que se preza, vou dar uma de ninja e usar o Bash pra mandar bem nessa! 🥷🥷

Minha estratégia é usar um script simples, mas eficiente, com foco em performance e otimização de recursos. 😅😅

Vou dar um passo a passo pra vocês, mas, vou deixar algumas coisas "em aberto", porque a graça é usar a criatividade e a inteligência pra criar um script que atenda às necessidades do teste. 😎😎

1. Criando um Script Minimalista:

Vamos começar com o script básico pra criar a API em Bash. Ele vai ter as funções de criação, leitura e contagem de pessoas:

#!/bin/bash

# Função para criar uma pessoa
create_pessoa() {
  apelido="$1"
  nome="$2"
  nascimento="$3"
  stack="$4"

  # Validação básica dos dados
  if [ -z "$apelido" ] || [ -z "$nome" ] || [ -z "$nascimento" ]; then
    echo "Apelido, nome e nascimento são obrigatórios."
    exit 1
  fi

  # Gera um UUID para a pessoa
  id=$(uuidgen)

  # Cria o arquivo da pessoa
  echo "{
  \"id\": \"$id\",
  \"apelido\": \"$apelido\",
  \"nome\": \"$nome\",
  \"nascimento\": \"$nascimento\",
  \"stack\": $stack
}" > pessoas/$id.json

  echo "Pessoa criada com sucesso! ID: $id"
}

# Função para ler uma pessoa por ID
read_pessoa() {
  id="$1"
  if [ -f "pessoas/$id.json" ]; then
    cat pessoas/$id.json
  else
    echo "Pessoa não encontrada."
  fi
}

# Função para buscar pessoas
search_pessoas() {
  termo="$1"

  # Busca pelos arquivos de pessoas
  find pessoas -name "*.json" -exec grep -q "$termo" {} \; -print0 | xargs -0 read_pessoa
}

# Função para contar pessoas
count_pessoas() {
  find pessoas -name "*.json" | wc -l
}

# Menu de opções
while true; do
  echo "
  1. Criar Pessoa
  2. Ler Pessoa por ID
  3. Buscar Pessoas
  4. Contar Pessoas
  5. Sair
  "

  read -p "Digite a opção: " opcao

  case "$opcao" in
    1)
      read -p "Digite o apelido: " apelido
      read -p "Digite o nome: " nome
      read -p "Digite a data de nascimento (AAAA-MM-DD): " nascimento
      read -p "Digite a stack (separe por vírgula): " stack
      create_pessoa "$apelido" "$nome" "$nascimento" "$stack"
      ;;
    2)
      read -p "Digite o ID: " id
      read_pessoa "$id"
      ;;
    3)
      read -p "Digite o termo da busca: " termo
      search_pessoas "$termo"
      ;;
    4)
      count_pessoas
      ;;
    5)
      echo "Saindo..."
      exit 0
      ;;
    *)
      echo "Opção inválida!"
      ;;
  esac
done
content_copy
Use code with caution.
Bash

2. Explicando o Código:

O código é bem simples, mas explicarei cada ponto crucial:

Função create_pessoa:

Recebe os dados da pessoa como argumentos (apelido, nome, nascimento e stack).

Faz uma validação básica dos dados para garantir que os campos obrigatórios estejam preenchidos.

Gera um UUID para a pessoa usando o comando uuidgen.

Cria um arquivo JSON com os dados da pessoa no diretório pessoas, usando o ID gerado como nome do arquivo.

Imprime uma mensagem confirmando a criação da pessoa.

Função read_pessoa:

Recebe o ID da pessoa como argumento.

Verifica se o arquivo da pessoa existe no diretório pessoas.

Se o arquivo existir, exibe o conteúdo do arquivo.

Se o arquivo não existir, imprime uma mensagem informando que a pessoa não foi encontrada.

Função search_pessoas:

Recebe o termo da busca como argumento.

Usa o comando find para buscar todos os arquivos JSON no diretório pessoas.

Usa o comando grep para filtrar os arquivos que contenham o termo da busca.

Usa o comando xargs para executar a função read_pessoa com os IDs dos arquivos encontrados.

Função count_pessoas:

Usa o comando find para buscar todos os arquivos JSON no diretório pessoas.

Usa o comando wc -l para contar o número de arquivos encontrados.

Menu de Opções:

Apresenta um menu com as opções disponíveis.

Lê a opção escolhida pelo usuário.

Executa a função correspondente à opção escolhida.

Repete o menu até que o usuário escolha a opção de sair.

3. Preparando a Rinha:

Agora que você já tem uma base de código, vamos nos preparar para a rinha:

Criar o diretório pessoas:

mkdir pessoas
content_copy
Use code with caution.
Bash

Construir a Imagem do Docker:
Você vai precisar criar um Dockerfile para sua aplicação.

FROM alpine:latest

RUN apk add bash \
    && apk add curl

COPY . /app
WORKDIR /app
RUN mkdir pessoas

CMD ["bash", "api.sh"]
content_copy
Use code with caution.
Dockerfile

Construir o Arquivo api.sh:
Crie um arquivo api.sh para o seu script Bash e coloque o conteúdo do script que criamos na etapa 1.

Criar o Arquivo docker-compose.yml:
Você vai precisar criar um arquivo docker-compose.yml com a configuração das suas APIs e do banco de dados. A configuração deve ter as restrições de recursos que definimos no início.

4. Submetendo o PR:

Crie um repositório público no GitHub com o seu código, e então faça um pull request para o repositório da Rinha de Backend, seguindo os passos:

Crie um repositório público no GitHub:

Acesse o site do GitHub e faça login.

Clique em "New repository"

Nomeie o repositório (ex: minha-api).

Crie o repositório.

Faça um pull request:

Acesse o repositório da Rinha de Backend (https://github.com/scoobiii/rinha-de-backend-2023-q3).

Clique em "Fork" para criar uma cópia do repositório na sua conta.

Acesse seu repositório (por exemplo: https://github.com/seu-usuario/rinha-de-backend-2023-q3).

Crie uma nova branch (ex: minha-solucao).

Adicione os arquivos da sua API (script bash, Dockerfile e docker-compose.yml).

Faça um commit com uma mensagem descritiva.

Vá até a página do repositório da Rinha de Backend (https://github.com/scoobiii/rinha-de-backend-2023-q3).

Clique em "New pull request".

Selecione a sua branch (ex: minha-solucao) como base e a branch original como comparativo.

Escreva uma mensagem descritiva do seu PR.

Submeta o PR.

Lembre-se:

Utilize os exemplos fornecidos no README para testar sua API e garantir que ela está funcionando corretamente.

Submeta seu PR até a meia-noite do dia 22/08.

Acompanhe a Rinha de Backend no dia 25/08.

Boa sorte! 🏆🏆

Observações:

Performance: É fundamental que você otimize sua API em termos de performance, principalmente por causa das restrições de recursos.

Estratégias: Aproveite a criatividade e a inteligência para criar um script que seja eficiente e que atenda às necessidades do teste.

Compartilhamento de Conhecimento: Não se esqueça de compartilhar seus conhecimentos e suas experiências com a comunidade.

Akita no comando! 😎😎

Espero que este guia te ajude na Rinha de Backend. 😉😉

#rinhabackend #akita #bash #coding #dev #performance #docker #github

--- START OF FILE RinhaBackendSimulation (1).scala ---

import scala.concurrent.duration._

import scala.util.Random

import io.gatling.core.Predef._
import io.gatling.http.Predef._

class RinhaBackendSimulation
extends Simulation {

val httpProtocol = http
.baseUrl("http://localhost:9999")
.userAgentHeader("Agente do Caos - 2023")

val criacaoEConsultaPessoas = scenario("Criação E Talvez Consulta de Pessoas")
.feed(tsv("pessoas-payloads.tsv").circular())
.exec(
http("criação")
.post("/pessoas").body(StringBody("#{payload}"))
.header("content-type", "application/json")
// 201 pros casos de sucesso :)
// 422 pra requests inválidos :|
// 400 pra requests bosta tipo data errada, tipos errados, etc. :(
.check(status.in(201, 422, 400))
// Se a criacao foi na api1 e esse location request atingir api2, a api2 tem que encontrar o registro.
// Pode ser que o request atinga a mesma instancia, mas estatisticamente, pelo menos um request vai atingir a outra.
// Isso garante o teste de consistencia de dados
.check(status.saveAs("httpStatus"))
.checkIf(session => session("httpStatus").as[String] == "201") {
header("Location").saveAs("location")
}
)
.pause(1.milliseconds, 30.milliseconds)
.doIf(session => session.contains("location")) {
exec(
http("consulta")
.get("#{location}")
)
}

val buscaPessoas = scenario("Busca Válida de Pessoas")
.feed(tsv("termos-busca.tsv").circular())
.exec(
http("busca válida")
.get("/pessoas?t=#{t}")
// qq resposta na faixa 2XX tá safe
)

val buscaInvalidaPessoas = scenario("Busca Inválida de Pessoas")
.exec(
http("busca inválida")
.get("/pessoas")
// 400 - bad request se não passar 't' como query string
.check(status.is(400))
)

setUp(
criacaoEConsultaPessoas.inject(
constantUsersPerSec(2).during(10.seconds), // warm up
constantUsersPerSec(5).during(15.seconds).randomized, // are you ready?

rampUsersPerSec(6).to(600).during(3.minutes) // lezzz go!!!
),
buscaPessoas.inject(
  constantUsersPerSec(2).during(25.seconds), // warm up
  
  rampUsersPerSec(6).to(100).during(3.minutes) // lezzz go!!!
),
buscaInvalidaPessoas.inject(
  constantUsersPerSec(2).during(25.seconds), // warm up
  
  rampUsersPerSec(6).to(40).during(3.minutes) // lezzz go!!!
)
content_copy
Use code with caution.

).protocols(httpProtocol)
}

<start_of_image> najboljsi akita

Vc vai participar com 6 solucoes,

bash, (evolua para conseguir competir e empatar com java)

prevayler,

lmax

disruptor

bash + prevyler + lmax

Escolha criar td simultaneamente

Use paython ou sh para automatizar a criacao de pastas arquivos testes, rodar os testes, refinar, vencer o stress teste mais de 1000000 inservoes em tres minutos
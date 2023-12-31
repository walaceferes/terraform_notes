# Terraform

Uma ferramenta de provisionamento de infraestrutura como código (IaC), porém, também pode provisionar configurações de ambientes e diversas plataformas SaaS como Pingdom e Opsgenie.

O grande diferencial do Terraform está na capacidade da ferramenta de guardar o estado de suas alterações, o que é chamado de estado. Isso permite que a ferramenta reconheça o que foi alterado por ela mesma, ao mesmo tempo que desconhece aquilo que não foi provisionado pelo Terraform.

É importante informar que o Terraform é uma ferramenta declarativa, ou seja, você apenas declara o que deseja provisionar, e o Terraform se encarrega de fazer as conexões, estabelecer a ordem do que será criado ou destruído primeiro, etc., tudo isso automaticamente, ao contrário de uma ferramenta procedural, onde é necessário informar "cada passo e a ordem dos mesmos".

## Entidades Principais
### hcl
HashiCorp Configuration Language, basicamente a linguagem utilizada para declarar os recursos que você deseja criar no Terraform. Nessa linguagem, você declara o que deseja criar seguindo sua sintaxe; isso inclui variáveis, módulos, etc.
#### bloco provider
É o bloco que se conecta com o provider, segue doc de todos os providers do terraform:
https://registry.terraform.io/browse/providers
#### bloco resource
É o bloco onde nós declaramos os recursos    que se deseja provisionar.
Para acessar um valor de um resource:

    tipo.nome.algum_output

#### Variables
O bloco de varíaveis é basicamente dessa forma:

    variable "nome_varivel" {
    type        = "descrever o tipo de variável, como string, number e etc"
    default     = "Estipula um valor padrão que é fixo, e sempre deve ser passado"
    description = "Opcional, para descrever a variável".
    }

Types:
* string
* number
* bool

Default:
Tem uma variável opcional com um valor fixado, se não utilizar o Default, o user é orbigado a passar um valor para essa variável.

Para acessar uma variável no Terraform, não é muito diferente de outras linguagens:
    
    var.nomedavariavel





#### Output
O Outoput na maioria das vezes ele é usado apenas apra retornar ao usuário algum valor, mensagem ou texto, ao falar de modulos, é que ele tem algumas funçṍes a mais, a principio, ele só obriga que seja declarado um valor.
    
    output "nome_output" {
        value = "valor que quer mostrar no output, podendo ser um resource, modulo ou variável"
    }

#### data
Mantém os dados de forma fixa para serem utilizados em outros locais

    data "tipo de provider" "nome" {
        //inputs
    }
#### module
Literalmente é o bloco que junta todos os outros em um modulo fechado e pode ser reutilizado e até mesmo "transportado".

    module "nome" {
        source = "caminho/para/o/modulo"
        //inputs
    }

* binário
* state

## Comandos

#### terraform init
A principio, esse é o primeiro comando a ser executado após a criação de uma estrutura em terrraform ou após clonar uma. O mesmo é responsável por baixar dependencias como plugins e modulos solicitados,criação de um diretório de trablho contendo diversos arquivos relevantes para para o funcionamento correto do Terraform(contendo versões e etc). O comando também inicializa o backend do terraform, que é responsável por armazenar o estado da infraestrutura gerenciada pelo Terraform.

    terraform init

# Módulo Terraform para Cluster EKS na AWS

Este projeto Terraform cria um cluster EKS (Elastic Kubernetes Service) na AWS, incluindo toda a infraestrutura necessária e componentes adicionais.

## Funcionalidades

- Cria uma VPC com subnets públicas e privadas.
- Configura um cluster EKS na VPC criada.
- Cria um grupo de nós gerenciado para o cluster EKS.
- Instala add-ons essenciais (CoreDNS, kube-proxy, vpc-cni, aws-ebs-csi-driver).
- Configura o AWS Load Balancer Controller.
- Gera e salva o arquivo kubeconfig do cluster.

## Pré-requisitos

- [Terraform](https://www.terraform.io/downloads.html) (versão 0.12 ou superior)
- [AWS CLI](https://aws.amazon.com/cli/) configurado com suas credenciais
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) (opcional, para interagir com o cluster após a criação)

## Estrutura do Projeto

- `main.tf`: Configuração principal do cluster EKS e VPC
- `variables.tf`: Definição de variáveis utilizadas no projeto
- `outputs.tf`: Outputs do Terraform após a criação dos recursos
- `providers.tf`: Configuração dos providers necessários
- `alb.tf`: Configuração do AWS Load Balancer Controller

## Como usar

1. Clone este repositório:

```
git clone https://github.com/Tech-Preta/terraform-aws-eks.git
```

2. Inicialize o Terraform:

```
terraform init
```

3. Revise o plano de execução:
```
terraform plan
```

4. Aplique as mudanças:
```
terraform apply
```

5. Após a conclusão, o arquivo kubeconfig será gerado no diretório do projeto. Use-o para se conectar ao cluster:

```
export KUBECONFIG=./kubeconfig_<nome-do-cluster>
kubectl get nodes
```

## Customização

Você pode personalizar o projeto modificando as variáveis em `variables.tf`. Algumas das principais variáveis incluem:

- `region`: Região da AWS onde o cluster será criado
- `cluster_name`: Nome do cluster EKS
- `cluster_version`: Versão do Kubernetes para o cluster
- `vpc_cidr`: CIDR block para a VPC
- `instance_types`: Tipos de instância EC2 para os nós do cluster

## Limpeza

Para destruir todos os recursos criados:

```
terraform destroy
```

## Notas

- Este projeto cria recursos na AWS que podem resultar em custos. Certifique-se de entender os custos associados antes de aplicar.
- O arquivo kubeconfig gerado contém informações sensíveis. Trate-o com cuidado e não o compartilhe publicamente.

## Contribuições

Contribuições são bem-vindas! Por favor, abra uma issue ou pull request para sugestões de melhorias ou correções.

## Licença

Este projeto está licenciado sob a [MIT License](LICENSE).
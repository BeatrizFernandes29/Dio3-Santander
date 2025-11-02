# Dio3-Santander

Este repositório faz parte do desafio proposto pela DIO, com o objetivo de aplicar e documentar os conhecimentos sobre AWS Step Functions.

O AWS Step Functions é um serviço da Amazon que permite criar fluxos de trabalho automatizados, coordenando diferentes serviços da AWS em etapas definidas.

Com ele, é possível:
- Orquestrar várias funções em sequência ou em paralelo;
- Automatizar processos sem precisar de um servidor dedicado;
- Visualizar e monitorar todo o fluxo de execução;
- Tratar erros e exceções de forma automática.

Um exemplo simples de uso seria:

1. O usuário envia um arquivo para o Amazon S3;  
2. Esse evento aciona uma função AWS Lambda;  
3. A função processa o arquivo (por exemplo, comprime ou analisa);  
4. O resultado é armazenado em outro bucket S3;  
5. O Step Functions coordena e monitora todas essas etapas.

Exemplo de definição JSON de um fluxo

```json
{
  "Comment": "Exemplo de Step Function simples",
  "StartAt": "ProcessarArquivo",
  "States": {
    "ProcessarArquivo": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:REGIAO:CONTA:function:ProcessarArquivo",
      "Next": "SalvarResultado"
    },
    "SalvarResultado": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:REGIAO:CONTA:function:SalvarResultado",
      "End": true
    }
  }
}

# Azure Event Hub - Function
 ## Pré-Requisitos
 
1. Conta do Azure: você precisa ter uma conta do Azure para criar um aplicativo de função do Azure e configurar o Event Hub. Se você não tiver uma conta do Azure, crie uma gratuitamente em https://azure.microsoft.com/pt-br/free/.

2. Visual Studio Code: você precisa ter o Visual Studio Code instalado em sua máquina. Se você ainda não o tiver instalado, faça o download e a instalação em https://code.visualstudio.com/.

3. Extensão do Azure Functions: você precisa ter a extensão do Azure Functions instalada no Visual Studio Code para criar e implantar a função do Azure. Você pode instalar a extensão clicando em "Extensões" no painel lateral do Visual Studio Code e pesquisando por "Azure Functions".

4. Node.js: você precisa ter o Node.js instalado em sua máquina para executar o ambiente de desenvolvimento local e implantar a função do Azure. Faça o download e a instalação em https://nodejs.org/en/.

5. Azure CLI: você precisa ter a Azure CLI instalada em sua máquina para criar e gerenciar recursos do Azure usando a linha de comando. Você pode fazer o download e a instalação em https://docs.microsoft.com/pt-br/cli/azure/install-azure-cli.

6. Conexão do Event Hub: você precisa ter uma conexão válida do Event Hub para configurar a função do Azure. Você pode criar um namespace do Event Hub e uma instância do Event Hub no portal do Azure e obter a conexão para configurar a função.

 ## Passo a passo
 
1. Abra o VS Code e crie uma nova pasta para o seu projeto. Em seguida, abra o terminal integrado do VS Code.

2. Execute o seguinte comando para criar uma nova função do Azure:

```
func init
```
3. Selecione a opção "Azure Functions" e escolha a linguagem "Javascript".

4. Em seguida, execute o seguinte comando para criar uma nova função de acionamento do Event Hub:

```
func new
```
5. Selecione a opção "Event Hub Trigger" e siga as instruções para configurar a função.
6. Abra o arquivo index.js criado na pasta ./eventHubTrigger e adicione o seguinte código para se conectar ao Event Hub:]
```
module.exports = async function (context, eventHubMessages) {
  context.log(`Event hub trigger function processed ${eventHubMessages.length} messages`);
  eventHubMessages.forEach(message => {
    context.log(`Processed message: ${JSON.stringify(message)}`);
  });
};
```
7. Substitua o nome da função pelo nome do seu Event Hub na seção de configuração do function.json:
```
{
  "bindings": [
    {
      "type": "eventHubTrigger",
      "name": "eventHubMessages",
      "direction": "in",
      "eventHubName": "<event-hub-name>",
      "connection": "<event-hub-connection-string>",
      "cardinality": "many",
      "consumerGroup": "$Default"
    }
  ]
}
```
8. Execute o seguinte comando para implantar a função no Azure:
```
func azure functionapp publish <function-app-name>
```
Certifique-se de substituir <function-app-name> pelo nome do seu aplicativo de função do Azure.

9. Depois que a implantação for concluída com êxito, vá para o portal do Azure e navegue até o aplicativo da função. Certifique-se de que a seção "Monitoramento" mostre que a função está em execução.

10. Agora, você pode enviar eventos para o Event Hub e a função será acionada automaticamente para processá-los. Você pode verificar os logs da função para ver os eventos que foram processados.

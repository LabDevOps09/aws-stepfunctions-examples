# Criando um Assistente de Delivery com AWS Step Functions e Amazon Bedrock 🏍️

Este projeto demonstra como construir um Assistente de Delivery que gerencia todo o fluxo de um pedido, desde a solicitação até a entrega, utilizando **AWS Step Functions** e integrando o **Amazon Bedrock** para fornecer uma experiência personalizada ao cliente.

## Cenário
Um cliente faz um pedido de comida em um aplicativo de delivery. O assistente gerencia o fluxo de ponta a ponta: valida o pedido, processa o pagamento, envia o pedido para o restaurante, monitora a entrega e interage com o cliente utilizando o **Amazon Bedrock** para fornecer sugestões personalizadas.

## 1. 🛒 Recebimento do Pedido

Quando o cliente faz um pedido por meio do aplicativo ou website, os dados do pedido (como itens, quantidade e endereço de entrega) são enviados para uma função **AWS Lambda**. Essa função é responsável por validar as informações do pedido, verificando se os dados inseridos estão corretos e completos. Caso haja algum erro, o processo retorna uma mensagem informando ao cliente o problema. Se o pedido estiver correto, ele avança para a etapa de validação do pagamento.

## 2. 💳 Validação do Pagamento

Após o pedido ser validado, uma nova função **Lambda** é acionada para realizar a verificação do pagamento. A função se conecta a um serviço de pagamento externo, como Stripe ou PayPal, para processar a transação e confirmar se o pagamento foi aprovado. Caso a transação seja bem-sucedida, o pedido é liberado para a próxima fase. Se houver falha no pagamento, o cliente é notificado e o pedido não é processado.

## 3. 🍽️ Processamento do Pedido

Com o pagamento validado, o pedido é enviado ao restaurante e o sistema atualiza seu status (ex.: "em preparo") no banco de dados **DynamoDB**. Nesse ponto, o **Amazon Bedrock** entra em ação para sugerir produtos adicionais ao cliente. Com base no histórico de pedidos, ele pode sugerir itens relevantes ou ofertas especiais, como sobremesas ou bebidas, incentivando compras adicionais e proporcionando uma experiência mais personalizada.

## 4. 🚚 Atualização do Status e Monitoramento da Entrega

Ao longo do processo de entrega, o status do pedido (como "em preparo", "a caminho" ou "entregue") é atualizado no **DynamoDB**. Além disso, o **Amazon Bedrock** pode ser utilizado para personalizar as notificações enviadas ao cliente, ajustando o tempo estimado de entrega com base no tráfego local ou outras variáveis externas. Isso garante que o cliente esteja sempre informado sobre o progresso de seu pedido de forma precisa e personalizada.

## 5. 📲 Notificação ao Cliente

Durante todo o processo, o cliente recebe notificações via **Amazon SNS** sobre o status do pedido, como "Seu pedido está sendo preparado" ou "Seu pedido está a caminho!". O **Amazon Bedrock** também é usado para enriquecer essas interações, permitindo que o sistema sugira ofertas, cupons de desconto ou outros produtos baseados no comportamento anterior do cliente. Um exemplo pode ser a sugestão de uma bebida complementar ao pedido ou uma oferta exclusiva, melhorando a experiência do usuário.  🔚


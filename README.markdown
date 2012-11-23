Ambiente de Testes para o PagSeguro - pagseguro-ambiente-testes
===============
Este software tem o objetivo de auxiliar o desenvolvedor a testar sua implementação PagSeguro de forma prática. É possível enviar o seu carrinho de compras do PagSeguro e simular o sistema de notificações. Atualmente, o jeito atual recomendado pelo PagSeguro é que se crie um vendedor falso e que então que o desenvolvedor compre manualmente produtos, via boleto ou cartão de crédito, o que se torna imprático na maioria das vezes. Este método impede o desenvolvedor de usar sua máquina local para testar o sistema de notificações, pois obviamente não é possível enviar uma notificação para um endereço local como 127.0.0.1. Além disso não é possível simular uma venda bem sucedida (a não ser que você realmente compre o produto). Com este sistema você conseguirá simular todos os tipos de notificações do PagSeguro de forma rápida e prática.

O código está em PHP e este é o único requerimento, fora isso é apenas necessário que o servidor tenha permissão para criar e modificar arquivos. Você pode usar o tradicional Apache para hospedar o seu servidor de testes.

Configurando o ambiente de testes
------------
É necessário configurar qual o endereço de retorno das notificações. Para isso abra o arquivo PagSeguroServer.php e configure as variáveis `$notification_domain`, `$notification_page` e `$notification_port` (tipicamente 80). Só isso! Agora basta enviar o seu request para a página `checkout.php`.

Como funciona
------------
Para iniciar o ambiente de testes é necessário que você primeiro envie os dados do seu carrinho de compras. Portanto em vez de enviar os dados para o PagSeguro, você enviará um request para a página `checkout.php`. Supondo que ela esteja na pasta `pagseguro` e esteja acessível através do `localhost`, seu request deverá ser feito para `localhost/pagseguro/checkout.php`. Após o request bem sucedido, as informações do seu request são salvas em um documento de texto para futuras consultas. Agora você já pode enviar a notificação que deseja para o seu servidor. Selecione que tipo de status a sua transação deve ter, por exemplo, "Aguardando Pagamento", "Paga" ou "Em disputa" e envie a notificação. Seu servidor receberá as informações da mesma forma que o PagSeguro as informaria: apenas o código na notificação e o tipo da notificação são enviados. Você pode agora solicitar os dados da transação enviado um pedido para o endereço `notifications.php`, com o código da notificação, seu e-mail de cadastro e token, assim como o PagSeguro exige. Pronto, você então receberá um documento `.xml` nos mesmos moldes do PagSeguro!

Fotos do Ambiente de Testes (Sandbox PagSeguro)
------------
Página inicial: http://i.imgur.com/VFZ0E.png
Carrinho enviado: http://i.imgur.com/NWFVO.png
Notificação enviada: http://i.imgur.com/8V4yf.png

Dúvida, problema ou sugestão? Quer contribuir?
------------
Crie um issue no GitHub! :)

Isenção de Responsabilidade
------------
Este software é gratuito e não está associado com o PagSeguro. PagSeguro é uma marca registrada da empresa UOL. Este ambiente de testes não é afiliado com a UOL e portanto não é um produto oficial do PagSeguro.

<h1>🚀 Sobre o desafio</h1>
<p>Nesse desafio, você deve continuar desenvolvendo a aplicação de gestão de transações, a GoFinances. Agora você irá praticar o que você aprendeu até agora no React.js junto com TypeScript, utilizando rotas e envio de arquivos por formulário.</p>
<p>Essa será uma aplicação que irá se conectar ao seu backend, e exibir as transações criadas e permitir a importação de um arquivo CSV para gerar novos registros no banco de dados.</p>
<h1>Preparando o backend</h1>
<p>Antes de tudo, para que seu frontend se conecte corretamente ao backend, vá até a pasta do seu backend e execute os comandos yarn add cors e depois yarn add @types/cors -D.</p>
<p>Depois disso vá até o seu app.ts ainda no backend, e importe o cors e adicione app.use(cors()) antes da linha que contém app.use(routes);</p>
<p>Além disso, tenha certeza que as informações da categoria, estão sendo retornadas junto com a transação do seu backend no formato como o seguinte:</p>
<pre>{
  "id": "c0512e43-6589-4dc8-bd0c-2a3f71b347aa",
  "title": "Loan",
  "type": "income",
  "value": "1500.00",
  "category_id": "d93eccc7-64bb-4268-b825-9200103f3a8b",
  "created_at": "2020-04-20T00:00:49.620Z",
  "updated_at": "2020-04-20T00:00:49.620Z",
  "category": {
    "id": "d93eccc7-64bb-4268-b825-9200103f3a8b",
    "title": "Others",
    "created_at": "2020-04-20T00:00:49.594Z",
    "updated_at": "2020-04-20T00:00:49.594Z"
  }
}</pre>
<p>Para isso, você pode utilizar a funcionalidade de eager loading do TypeORM, adicionando o seguinte na sua model de transactions:</p>
<pre>@ManyToOne(() => Category, category => category.transaction, { eager: true })
@JoinColumn({ name: 'category_id' })
category: Category;</pre>
<p>Lembre também de fazer o mesmo na model de Category, mas referenciando a tabela de Transaction.</p>
<pre>@OneToMany(() => Transaction, transaction => transaction.category)
transaction: Transaction;</pre>
<h1>Funcionalidades da aplicação</h1>
<p>Agora que você já está com o template clonado e pronto para continuar, você deve verificar os arquivos da pasta src e completar onde não possui código, com o código para atingir os objetivos de cada rota.</p>
<ul>
<li>
<strong>Listar as transações da sua API:</strong> Sua página Dashboard deve ser capaz de exibir uma listagem através de uma tabela, com o campo title, value, type e category de todas as transações que estão cadastradas na sua API.
</li>
<li>
<strong>Importar arquivos CSV:</strong> Na sua página Import, você deve permitir o envio de um arquivo no formato csv para o seu backend, que irá fazer a importação das transações para o seu banco de dados.
</li>
</ul>
<p><strong>Dica 1:</strong> Deixamos disponível um componente chamado Upload na pasta components para você ter já preparado uma opção de drag-n-drop para o upload de arquivos. PS: Caso você esteja no windows e esteja sofrendo com algum erro ao tentar importar CSV, altere o tipo de arquivo dentro do arquivo components/upload/index.ts de text/csv para .csv, application/vnd.ms-excel, text/csv.</p>
<p><strong>Dica 2:</strong> Utilize o FormData() para conseguir enviar o seu arquivo para o seu backend.</p>
<h1>Específicação dos testes</h1>
<p>Em cada teste, tem uma breve descrição no que sua aplicação deve cumprir para que o teste passe.</p>
<p>Para esse desafio, temos os seguintes testes:</p>
<ul>
<li>
<strong>should be able to list the total balance inside the cards:</strong> Para que esse teste passe, sua aplicação deve permitir que seja exibido na sua Dashboard, cards contendo o total de income, outcome e o total da subtração de income - outcome que são retornados pelo balance do seu backend.
</li>
<li>
<strong>should be able to list the transactions:</strong> Para que esse teste passe, sua aplicação deve permitir que sejam listados dentro de uma tabela, toda as transações que são retornadas do seu backend.
</li><br>
<p><strong>Dica:</strong> Para a exibição dos valores na listagem de transações, as transações com tipo income devem exibir os valores no formado R$ 5.500,00. Transações do tipo outcome devem exibir os valores no formado - R$ 5.500,00.</p>
<li>
<strong>should be able to navigate to the import page:</strong> Para que esse teste passe, você deve permitir a troca de página através do Header, pelo botão que contém o nome Importar.
</li><br>
<p><strong>Dica:</strong> Utilize o componente Link que é exportado do react-router-dom, passando a propriedade to que leva para a página /import.</p>
<li>
<strong>should be able to upload a file:</strong> Para que esse teste passe, você deve permitir que um arquivo seja enviado através do componente de drag-n-drop na página de import, e que seja possível exibir o nome do arquivo enviado para o input.
</li><br>
<p><strong>Dica:</strong> Deixamos disponível um componente chamado FileList na pasta components para ajudar você a listar os arquivos que enviar pelo componente de Upload, ele deve exibir o título do arquivo e o tamanho dele.</p>
</ul>
<h1>📆 Entrega</h1>
<p>Esse desafio deve ser entregue a partir da plataforma da Rocketseat, envie o link do repositório que você fez suas alterações. Após concluir o desafio, fazer um post no Linkedin e postar o código no Github é uma boa forma de demonstrar seus conhecimentos e esforços para evoluir na sua carreira para oportunidades futuras.</p>

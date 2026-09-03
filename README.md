# Anybank

Aplicacao web de uma conta bancaria simples, desenvolvida com Angular. O usuario pode registrar depositos e saques, acompanhar o saldo da conta corrente e consultar o extrato das transacoes realizadas.

## Funcionalidades

- Exibe uma saudacao com a data atual.
- Mostra o saldo formatado em reais (BRL).
- Permite criar transacoes dos tipos `Deposito` e `Saque`.
- Valida o tipo e o valor da transacao no formulario.
- Impede saques com valor maior que o saldo disponivel.
- Lista as transacoes da mais recente para a mais antiga.
- Exibe uma mensagem quando ainda nao existem transacoes.

## Tecnologias

- Angular 19 com componentes standalone.
- TypeScript 5.6.
- Angular Signals para o estado das transacoes e o saldo calculado.
- Angular Forms com `ngModel`.
- RxJS e Zone.js, fornecidos pela plataforma Angular.
- `nanoid` para gerar o identificador de cada transacao.
- Jasmine e Karma configurados para testes unitarios.

## Pre-requisitos

- Node.js compativel com as dependencias do projeto.
- npm.

Nao e necessario instalar o Angular CLI globalmente: os comandos usam a versao local declarada no projeto.

## Instalacao

```bash
npm install
```

## Desenvolvimento

Inicie o servidor local com:

```bash
npm start
```

Depois, acesse [http://localhost:4200](http://localhost:4200). O servidor recarrega a aplicacao automaticamente durante o desenvolvimento.

## Scripts disponiveis

| Comando | Descricao |
| --- | --- |
| `npm start` | Inicia o servidor de desenvolvimento com `ng serve`. |
| `npm run build` | Gera o build de producao em `dist/anybank`. |
| `npm run watch` | Gera o build em modo desenvolvimento e observa alteracoes. |
| `npm test` | Executa os testes configurados com Angular/Karma. |
| `npm run ng -- <comando>` | Executa diretamente um comando da Angular CLI. |

## Como funciona

O componente raiz mantem a lista de transacoes em um `signal`. O saldo e derivado dessa lista: depositos somam ao saldo e saques subtraem. Quando um saque ultrapassa o saldo atual, a transacao nao e adicionada e a aplicacao informa `Saldo insuficiente!`.

Cada transacao armazena:

- um identificador gerado com `nanoid`;
- o tipo (`Deposito` ou `Saque`);
- o valor numerico;
- a data e hora de criacao.

## Estrutura principal

```text
src/
	app/
		app.component.*              Composicao da tela e regra do saldo
		banner/                      Saudacao, data e saldo da conta
		form-nova-transacao/         Formulario de deposito ou saque
		extrato/                     Lista de transacoes
			transacao/                 Apresentacao de cada transacao
		modelos/transacao.ts         Modelo e tipos de transacao
	main.ts                         Inicializacao da aplicacao
	styles.css                      Estilos globais
public/                            Assets publicos, como o favicon
```

## Limitacoes atuais

- Os dados ficam somente em memoria e sao perdidos ao recarregar a pagina.
- Nao ha backend, banco de dados, autenticacao ou integracao com uma conta real.
- O nome exibido na saudacao esta definido diretamente na interface.
- O repositorio possui a configuracao de testes do Angular, mas nao inclui arquivos de testes especificos no momento.

### Compatibilidade das dependencias

As dependencias principais e as ferramentas de build do Angular estao alinhadas na versao 19. Se o ambiente local estiver com uma instalacao antiga, execute `npm install` antes de iniciar o projeto.

## Build de producao

Para gerar os arquivos otimizados:

```bash
npm run build
```

O resultado sera salvo em `dist/anybank`.

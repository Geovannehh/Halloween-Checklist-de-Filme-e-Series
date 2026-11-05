<!-- HALLOWEEN-SCREENSHOTS-START -->
# EquaGuard — Halloween e checklist de outubro

Edição com calendário de 31 filmes, sugestões de Fanta e checklist dos dez filmes e séries das imagens enviadas. As marcações de assistidos ficam salvas no navegador, separadamente em cada lista.

## Como abrir

1. Extraia o ZIP inteiro, mantendo a estrutura de pastas.
2. No Windows, execute `INICIAR_EQUAGUARD.cmd`. É necessário ter Python instalado; o inicializador prepara o ambiente e instala o Flask, com acesso à internet na primeira execução.
3. Aguarde a abertura automática do navegador. O endereço padrão é `http://127.0.0.1:3000/#inicio`; se a porta estiver ocupada, o inicializador informa outra porta.
4. Caso seja solicitado, escolha um perfil fictício de demonstração. Mantenha o servidor aberto enquanto usa o site.

## Telas do site

Capturas reais da versão local, realizadas em 5 de novembro de 2026. As imagens estão na pasta `docs/telas/` e podem ser abertas diretamente após extrair o ZIP.

### Página inicial de Halloween

![Página inicial de Halloween](docs/telas/01-inicio.jpg)

### Checklist de outubro

Dez títulos das fotos enviadas, com contador e opção “Já assisti”. Datas e plataformas foram transcritas das imagens e podem mudar.

![Checklist de filmes e séries de outubro](docs/telas/02-checklist-outubro.jpg)

### Calendário de 31 filmes

Um filme por dia, filtro de intensidade e progresso de assistidos. Intensidade editorial não substitui classificação etária.

![Calendário de filmes](docs/telas/03-calendario.jpg)

### Acesso à plataforma EquaGuard

![Apresentação da plataforma](docs/telas/04-plataforma.jpg)

### Página de Halloween completa

A captura abaixo reúne também a seção Fanta e todos os títulos das duas listas.

![Página completa de Halloween](docs/telas/00-pagina-completa.jpg)

## Conteúdo do pacote

Código-fonte, recursos visuais, fontes, testes, documentação e capturas de tela. Ambiente virtual, banco de dados local, dados de sessão e arquivos de configuração privados não acompanham o pacote.

<!-- HALLOWEEN-SCREENSHOTS-END -->

---

# EquaGuard

Plataforma educacional de cibersegurança com lições, simulações, recomendações, conquistas e o Escape Room **Guardiões da Energia Digital**. Projeto demonstrativo da equipe 237, adaptado da base Conecta Campus.

## Executar no Windows

Requer Python 3.10 ou superior. Abra `INICIAR_EQUAGUARD.cmd` e acesse http://127.0.0.1:3000. Na primeira execução, o inicializador cria `.venv` e instala o Flask. Mantenha o terminal aberto; Ctrl+C encerra o servidor.

Execução manual, no PowerShell:

```powershell
py -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe flask_app.py
```

Não é necessário Node.js para usar a aplicação. Para outra porta, defina `$env:PORT='5001'` antes de iniciar. As configurações disponíveis estão em `.env.example`; o arquivo é uma referência e não é carregado automaticamente.

## Estrutura

```text
equaguard/
    __init__.py          fábrica create_app()
    config.py            configuração e sessão
    database.py          conexão SQLite por contexto
    http.py              proteção e validação das requisições
    schema.sql           tabelas e índices
    content/             lições, cenários e salas
    routes/              blueprints da API e páginas
    services/            progresso, indicadores e estado das partidas
    static/              módulos JavaScript, CSS e imagens
    templates/           página principal e parciais Jinja
tests/                   testes com bancos temporários
scripts/                 ferramentas de manutenção
docs/architecture.md     decisões de organização
legacy/conecta-campus/   arquivos da aplicação anterior
backups/                 cópias de recuperação locais
instance/                banco e segredo da sessão
flask_app.py             entrada local e WSGI
```

## Funcionalidades

- Perfis fictícios de campo, atendimento e administrativo, nos modos colaborador e gestão.
- Diagnóstico inicial, cinco lições interativas e comparação pré/pós.
- Simulações em duas etapas; a primeira escolha determina a situação seguinte. O falso suporte é um desafio avançado.
- GuardIA com FAQ por palavras-chave e recomendações priorizadas pelas dificuldades registradas.
- XP, quatro níveis, sete conquistas, histórico e proteção contra recompensa duplicada.
- Indicadores agregados de participação, conclusão, acertos, reporte, evolução e recomendações.
- Escape Room local para 2 a 6 pessoas, com cinco salas, evidências e protocolo final.

### Regras da missão

A equipe escolhe 20 ou 30 minutos. O cronômetro continua ao atualizar ou trocar de módulo. Uma decisão incorreta desconta 30 segundos; uma dica desconta 60 segundos, uma vez por sala. O servidor valida a ordem, o prazo e as respostas. A primeira vitória concede 250 XP ao perfil que iniciou a partida. Há revisão educativa na vitória e ao esgotar o tempo. Novas tentativas não duplicam XP.

### Progresso e persistência

Diagnóstico: 30 XP; lição correta: 50 XP; simulação: 80 XP na primeira decisão e 40 XP na segunda; melhora no pós-teste: 60 XP. Níveis: Explorador (0), Sentinela (150), Defensor (350) e Guardião (600). Erros não retiram XP.

O SQLite usa `instance/equaguard.db`; o segredo da sessão fica em `instance/.equaguard_secret`. Esses caminhos foram preservados na reorganização. O cookie mantém o perfil neste navegador por até 30 dias. Outro navegador ou a limpeza dos cookies pode criar outra identidade demonstrativa.

## Testes e manutenção

```powershell
.\.venv\Scripts\python.exe -m unittest discover -s tests -v
```

Os testes cobrem sessão, CSRF, validação, pontuação, recomendações, isolamento, persistência, prazo e conclusão da missão. Cada teste usa seu próprio banco temporário.

Para formatar o código:

```powershell
.\.venv\Scripts\python.exe -m pip install -r requirements-dev.txt
.\.venv\Scripts\python.exe scripts/format_code.py
```

Se houver Node.js instalado, `node scripts/check_frontend.cjs` verifica a sintaxe e os caminhos dos módulos JavaScript. `.editorconfig` define a indentação e codificação. Consulte `docs/architecture.md` antes de alterar a comunicação entre módulos.

## Jogo integrado

A opção **Missão interativa**, no menu e em Praticar, abre diretamente https://equaguard-versao-ii-production.up.railway.app/. O jogo mantém pontuação própria e requer internet.

## Limites da demonstração

O seletor de gestão não é autenticação corporativa. A GuardIA não utiliza IA generativa. Não há SSO, integração com sistemas internos, envio real de e-mails, coleta de credenciais, monitoramento de colaboradores ou multiplayer entre dispositivos. Os cenários são fictícios; o projeto não é um produto oficial da Equatorial.

O servidor aceita conexões em `0.0.0.0`, sem debug, e usa a variável `PORT` (padrão: 3000). O inicializador abre o navegador em `127.0.0.1`. `/health` informa o estado do serviço. A configuração WSGI opcional está em `pythonanywhere_wsgi.py`.

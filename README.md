# 🏐 Peladas de Vôlei - Ao Vivo

Aplicação web responsiva para gerenciar, organizar e acompanhar partidas informais de voleibol em tempo real. Sistema completo com autenticação, criação de times, registro de pontuações e exportação de resultados.

---

## 📋 Índice

- [Visão Geral](#visão-geral)
- [Funcionalidades](#funcionalidades)
- [Pré-requisitos](#pré-requisitos)
- [Instalação](#instalação)
- [Como Usar](#como-usar)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Tecnologias](#tecnologias)
- [Configuração do Backend](#configuração-do-backend)
- [Contribuindo](#contribuindo)
- [Suporte](#suporte)
- [Licença](#licença)

---

## 🎯 Visão Geral

**Peladas de Vôlei** é uma solução intuitiva para gerenciadores de quadras e organizadores de partidas. A aplicação permite:

- ✅ Criar e gerenciar times de forma rápida
- ✅ Registrar pontuações em tempo real
- ✅ Acompanhar agenda de jogos
- ✅ Exportar resultados em PDF
- ✅ Controle de acesso com autenticação
- ✅ Interface responsiva (mobile, tablet, desktop)

Desenvolvido com foco em **usabilidade**, **performance** e **acessibilidade**.

---

## ✨ Funcionalidades

### 👥 Gerenciamento de Times
- Criar times com nome e quantidade de jogadores
- Adicionar/remover jogadores de um time
- Visualizar composição completa de cada time
- Assignação automática de cores para diferenciação visual

### 🎮 Controle de Partidas
- Registrar pontuação em tempo real
- Incrementar/decrementar pontos facilmente
- Visualizar placar ao vivo
- Histórico de partidas e estatísticas

### 📅 Agenda
- Criar agenda de próximas partidas
- Editar horários e adversários
- Marcar partidas como completas
- Visualizar próximas 10 partidas programadas

### 📊 Exportação
- Gerar PDF com resultados da partida
- Captura de tela da interface
- Download direto para dispositivo do usuário

### 🔐 Autenticação e Segurança
- Login com autenticação via Supabase
- Dois modos: **Admin** (edição) e **Espectador** (visualização)
- Persistência de sessão
- Dados sincronizados em tempo real

### 🎨 Interface Moderna
- Design dark mode com tema verde
- Responde a todos os tamanhos de tela
- Animações suaves e transições
- Sombras e profundidade visual
- Tipografia clara e legível

---

## 📦 Pré-requisitos

- **Navegador moderno**: Chrome 90+, Firefox 88+, Safari 14+, Edge 90+
- **Conexão com internet** (para sincronização com Supabase)
- **Supabase account**: Necessário para autenticação (gratuito)

### Dependências Externas (via CDN)
- HTML2Canvas v1.4.1 - Captura de tela
- html2pdf v0.9.3 - Geração de PDF
- Supabase JS v2 - Backend e autenticação
- Google Fonts (Inter) - Tipografia

---

## 🚀 Instalação

### 1. Clonar o Repositório
```bash
git clone https://github.com/jppaztech/valenovolei.git
cd valenovolei
```

### 2. Configurar Supabase
Acesse [supabase.com](https://supabase.com) e crie um novo projeto:

1. Crie uma nova tabela `users`:
```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  email TEXT UNIQUE NOT NULL,
  role TEXT DEFAULT 'admin',
  created_at TIMESTAMP DEFAULT NOW()
);
```

2. Crie uma tabela `games`:
```sql
CREATE TABLE games (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  team1_name TEXT NOT NULL,
  team2_name TEXT NOT NULL,
  team1_score INTEGER DEFAULT 0,
  team2_score INTEGER DEFAULT 0,
  created_at TIMESTAMP DEFAULT NOW(),
  status TEXT DEFAULT 'pending'
);
```

3. Copie suas credenciais (URL e Anon Key) do dashboard do Supabase

### 3. Configurar Credenciais
Edite o arquivo `index.html` e localize a seção de inicialização do Supabase:

```javascript
// Substitua com suas credenciais do Supabase
const supabaseUrl = 'YOUR_SUPABASE_URL';
const supabaseKey = 'YOUR_SUPABASE_ANON_KEY';
```

### 4. Servir Localmente (Opcional)
Para desenvolvimento, use um servidor local:

```bash
# Usando Python 3
python -m http.server 8000

# Ou usando Node.js (http-server)
npx http-server

# Ou usando Ruby
ruby -run -ehttpd . -p8000
```

Acesse: `http://localhost:8000`

### 5. Deploy
- **Netlify**: Conecte o repositório Git diretamente
- **Vercel**: Similar ao Netlify, com CI/CD automático
- **GitHub Pages**: Requer push simples se usando conta pessoal
- **Servidor próprio**: Copie os arquivos para seu servidor web

---

## 💻 Como Usar

### Fluxo Básico

#### 1. **Fazer Login**
   - Clique em "Admin Login" no canto superior direito
   - Insira suas credenciais
   - Você estará no modo **Edição**

#### 2. **Cadastrar Times**
   - Preencha o nome do time na seção "Cadastro"
   - Defina o número de jogadores
   - Clique em "Adicionar Time"
   - O time aparecerá na lista de times ativos

#### 3. **Iniciar Partida**
   - Escolha dois times na seção "Partida Atual"
   - Clique em "Iniciar Partida"
   - O placar aparecerá com a pontuação zerada

#### 4. **Registrar Pontuação**
   - Use os botões `+` e `-` para adicionar/remover pontos
   - Ou digite diretamente no campo de pontuação
   - A atualização é em tempo real

#### 5. **Finalizar Partida**
   - Clique em "Finalizar Partida"
   - Os dados são salvos automaticamente

#### 6. **Agendar Próximas Partidas**
   - Na seção "Agenda", preencha os times adversários
   - Defina horário e local
   - Clique em "Agendar"

#### 7. **Exportar Resultado**
   - Clique em "Exportar para PDF"
   - Seu navegador fará download automaticamente

### Dicas Práticas
- 💡 Modo **Espectador** permite que todos acompanhem sem editar
- 💡 Dados persistem no banco de dados (Supabase)
- 💡 Interface funciona offline com dados em cache
- 💡 Use em TV/projetor para visualização em tempo real

---

## 📁 Estrutura do Projeto

```
valenovolei/
├── index.html          # Aplicação SPA (Single Page Application)
├── README.md           # Este arquivo
├── .git/               # Histórico de versões
└── package.json        # (Opcional) Para dependências Node
```

### Divisão de Código (em index.html)

```html
<!-- Seção de Estilos (CSS) -->
<style>
  /* Variáveis CSS */
  /* Layout base */
  /* Componentes */
  /* Responsividade */
</style>

<!-- Seção de Interface (HTML) -->
<body>
  <header>...</header>
  <main>...</main>
</body>

<!-- Seção de Lógica (JavaScript) -->
<script>
  // Inicialização Supabase
  // Funções de autenticação
  // Gerenciamento de times
  // Controle de pontuação
  // Exportação de PDF
</script>
```

---

## 🛠️ Tecnologias

### Frontend
- **HTML5** - Marcação semântica
- **CSS3** - Design responsivo com Grid e Flexbox
- **JavaScript (ES6+)** - Lógica de aplicação
- **Inter Font** - Tipografia via Google Fonts

### Backend & Banco de Dados
- **Supabase** - PostgreSQL + API real-time
- **Autenticação** - Supabase Auth
- **Real-time** - WebSockets para sincronização

### Bibliotecas Externas
- **html2canvas** - Captura de elementos DOM
- **html2pdf** - Conversão de HTML para PDF
- **Supabase JS** - SDK JavaScript oficial

### Deploy
- **Git** - Controle de versão
- **GitHub** - Hospedagem de código
- **Netlify/Vercel** - Hospedagem da aplicação

---

## ⚙️ Configuração do Backend

### Variáveis de Ambiente
Crie um arquivo `.env` (se usando build tool):
```env
VITE_SUPABASE_URL=https://seu-projeto.supabase.co
VITE_SUPABASE_ANON_KEY=sua-chave-anonima
```

### Políticas de Segurança (RLS)
No Supabase, configure Row-Level Security:

```sql
-- Permitir leitura pública de games
ALTER TABLE games ENABLE ROW LEVEL SECURITY;

CREATE POLICY "Games visíveis para todos"
ON games FOR SELECT
USING (true);

-- Apenas admins podem editar
CREATE POLICY "Apenas admins editam games"
ON games FOR UPDATE
USING (auth.role() = 'admin');
```

### Sincronização em Tempo Real
A aplicação usa Supabase Realtime para sincronizar dados entre múltiplos usuários automaticamente.

---

## 🤝 Contribuindo

Contribuições são bem-vindas! Para contribuir:

### 1. Fork o Repositório
```bash
git clone https://github.com/seu-usuario/valenovolei.git
```

### 2. Criar Branch de Feature
```bash
git checkout -b feature/sua-feature
```

### 3. Fazer Alterações
- Mantenha o código limpo e bem comentado
- Teste em múltiplos navegadores
- Verifique responsividade

### 4. Commit e Push
```bash
git add .
git commit -m "feat: descrição da sua feature"
git push origin feature/sua-feature
```

### 5. Abrir Pull Request
Descreva suas mudanças e por que devem ser mergeadas.

### Diretrizes
- ✅ Código limpo e bem documentado
- ✅ Sem console.log em produção
- ✅ Respeitar design system existente
- ✅ Testar em mobile também
- ✅ Atualizar README se necessário

---

## 🐛 Suporte

Encontrou um bug? Tem uma sugestão?

- **Issues**: [GitHub Issues](https://github.com/jppaztech/valenovolei/issues)
- **Discussões**: [GitHub Discussions](https://github.com/jppaztech/valenovolei/discussions)
- **Email**: Abra uma issue com a tag `[SUPORTE]`

### FAQ

**P: Posso usar offline?**  
R: Parcialmente. Os dados em cache são acessíveis, mas sincronização é online.

**P: Quantos times posso criar?**  
R: Ilimitado, apenas o desempenho do navegador é o limite.

**P: Como resetar minha senha?**  
R: Use a opção "Esqueci minha senha" na tela de login do Supabase.

**P: Posso customizar cores?**  
R: Sim! Edite as variáveis CSS no topo do arquivo `index.html`.

---

## 📄 Licença

Este projeto está licenciado sob a **MIT License** - veja o arquivo LICENSE para detalhes.

```
MIT License

Copyright (c) 2024 jppaztech

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.
```

---

## 👨‍💻 Autor

**jppaztech**
- GitHub: [@jppaztech](https://github.com/jppaztech)
- Projeto criado para facilitar a organização de peladas de vôlei

---

## 🙏 Agradecimentos

- ❤️ Supabase pela plataforma de backend excelente
- ❤️ Comunidade open source
- ❤️ Todos os contribuidores

---

## 📊 Status do Projeto

- ✅ v1.0 - Fase de teste de produção
- 🚧 v1.1 - Estatísticas avançadas (em desenvolvimento)
- 🔄 v1.2 - App mobile nativa (planejado)
- 💡 v2.0 - Sistema de torneios (futuro)

---

<div align="center">

**⭐ Se este projeto foi útil, não esqueça de dar uma estrela!**

[GitHub](https://github.com/jppaztech/valenovolei) • [Issues](https://github.com/jppaztech/valenovolei/issues) • [Discussões](https://github.com/jppaztech/valenovolei/discussions)

</div>

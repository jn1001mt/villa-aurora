# Villa Aurora — Espaço de Eventos & Buffet

> **Aviso de Caráter Acadêmico:** Este projeto é uma aplicação web desenvolvida para fins estritamente didáticos e acadêmicos. Todos os dados comerciais apresentados — incluindo valores de pacotes, capacidade de lotação, números de telefone, endereços, links de redes sociais e e-mails — são meramente demonstrativos e fictícios.

---

## 🏛️ Sobre o Projeto

O **Villa Aurora** é um website institucional e comercial de alto padrão desenvolvido com o framework [Astro](https://astro.build/). O projeto foi concebido para divulgar um espaço exclusivo para eventos sociais e corporativos (casamentos, festas de 15 anos, formaturas e celebrações corporativas) integrado a um serviço próprio de alta gastronomia e buffet autoral em São Paulo - SP.

O design do projeto prioriza uma atmosfera sofisticada, utilizando uma paleta cromática em tons terrosos escuros (*deep taupe*), detalhes em bronze e ouro suave, tipografia clássica com *Cormorant Garamond* e *Montserrat*, além de backgrounds em vídeo imersivos e múltiplos pontos de conversão para atendimento consultivo via WhatsApp.

---

## 🌐 Status do Projeto

* **Design e Funcionamento:** Aprovados e publicados.
* **Ambiente de Produção:** Ativo.

---

## 🚀 Tecnologias e Ferramentas

* **Framework Principal:** [Astro](https://astro.build/) (v7.x)
* **Linguagens:** HTML5 Semântico, CSS3 Moderno (Scoped CSS) e TypeScript / Vanilla JavaScript
* **Tipografia:** Google Fonts ([Cormorant Garamond](https://fonts.google.com/specimen/Cormorant+Garamond) e [Montserrat](https://fonts.google.com/specimen/Montserrat))
* **Mídias:** Vídeos em MP4 otimizados para reprodução contínua em loop e fotografias de alta resolução
* **Ambiente de Execução:** Node.js `>= 22.23.4`

---

## 🗺️ Páginas e Estrutura de Rotas

O projeto conta com **7 páginas ativas**:

| Rota | Arquivo Fonte | Descrição |
| :--- | :--- | :--- |
| `/` | `src/pages/index.astro` | Página inicial com hero em vídeo, história, destaques dos espaços, resumo gastronômico, modalidades e depoimentos. |
| `/ambientes` | `src/pages/ambientes.astro` | Apresentação detalhada dos espaços (Salão Nobre, Jardim, Lounge Bar, Pista e Camarim) e tabela de capacidades. |
| `/eventos` | `src/pages/eventos.astro` | Modalidades de eventos atendidos (Casamentos, 15 Anos, Aniversários, Formaturas e Corporativos). |
| `/galeria` | `src/pages/galeria.astro` | Mosaico de fotos com filtro interativo de categorias via JavaScript. |
| `/pacotes` | `src/pages/pacotes.astro` | Planos de contratação (Essencial, Clássico, Premium e Exclusivo) e comparativo de serviços. |
| `/buffet` | `src/pages/buffet.astro` | Filosofia da gastronomia autoral, formatos de serviço (empratado, ilhas e volante), cardápios e degustação. |
| `/contato` | `src/pages/contato.astro` | Formulário detalhado de solicitação de proposta, dados de localização em São Paulo e FAQ. |

---

## 📁 Estrutura de Diretórios

```text
teste/
├── public/                       # Mídias estáticas servidas diretamente
│   ├── buffet-villa-aurora.mp4  # Vídeo temático de gastronomia
│   ├── espaco-villa-aurora.mp4  # Vídeo dos ambientes
│   ├── hero-villa-aurora.mp4    # Vídeo principal da página inicial
│   ├── favicon.ico              # Favicon tradicional
│   └── favicon.svg              # Favicon vetorial
├── src/
│   ├── assets/                  # Assets estáticos
│   ├── components/              # Componentes da interface
│   │   ├── Header.astro         # Barra de navegação e menu mobile
│   │   ├── Footer.astro         # Rodapé institucional em 4 colunas
│   │   ├── WhatsAppButton.astro # Botão flutuante de atendimento rápido
│   │   └── Welcome.astro        # Componente auxiliar de template
│   ├── layouts/
│   │   └── Layout.astro         # Layout base Astro
│   └── pages/                   # Rotas da aplicação (7 páginas)
├── AGENTS.md                     # Diretrizes de desenvolvimento e agentes
├── AUDITORIA.md                  # Registro formal da auditoria técnica do código
├── briefing.md                   # Briefing de posicionamento e negócio da Villa Aurora
├── mapa-site.md                  # Mapa da arquitetura da informação e taxonomia
├── REFINAMENTO.md                # Roteiro e backlog planejado para evoluções futuras
├── package.json                  # Dependências e scripts do projeto
├── astro.config.mjs              # Configuração do framework Astro
└── tsconfig.json                 # Configuração do compilador TypeScript
```

---

## 🛠️ Instalação e Execução Local

### Pré-requisitos
* Node.js versão `22.23.4` ou superior.
* Gerenciador de pacotes `npm`.

### Passo a Passo

1. **Instalar dependências:**
   ```bash
   npm install
   ```

2. **Iniciar o servidor de desenvolvimento:**
   * Modo interativo:
     ```bash
     npm run dev
     ```
   * Modo background (conforme recomendado em `AGENTS.md`):
     ```bash
     astro dev --background
     ```
     *(Gerenciável via `astro dev status`, `astro dev logs` e `astro dev stop`).*

3. **Acessar a aplicação no navegador:**
   ```
   http://localhost:4321
   ```

4. **Gerar a build estática de produção:**
   ```bash
   npm run build
   ```

5. **Visualizar a build localmente:**
   ```bash
   npm run preview
   ```

---

## 📚 Documentação Complementar

Para compreender a fundo o planejamento, a arquitetura e as análises técnicas do projeto, consulte os documentos dedicados na raiz do repositório:

* **[`briefing.md`](./briefing.md):** Posicionamento, proposta de valor, personas e pilares de serviços.
* **[`mapa-site.md`](./mapa-site.md):** Estrutura minuciosa de cada página, seções e fluxo de conversão.
* **[`AUDITORIA.md`](./AUDITORIA.md):** Diagnóstico detalhado de padrões de código, estilos e manutenibilidade.
* **[`REFINAMENTO.md`](./REFINAMENTO.md):** Roadmap com 7 frentes de evolução futura sem alterar o design atual.
* **[`AGENTS.md`](./AGENTS.md):** Instruções operacionais para agentes de IA e desenvolvedores.

---

## ⚖️ Licença e Uso

Este projeto foi criado estritamente para finalidades educacionais e de demonstração prática de desenvolvimento web com Astro. Todas as informações comerciais são fictícias.

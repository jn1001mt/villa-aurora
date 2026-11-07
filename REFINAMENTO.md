# Documento de Refinamento e Roadmap Futuro — Villa Aurora

> **Nota de Contexto e Escopo:** Este documento consolida o planejamento de melhorias, refatorações técnicas e expansões funcionais para o projeto **Villa Aurora**. O design e funcionamento atuais já foram aprovados e publicados. **Nenhuma das melhorias sugeridas abaixo foi implementada nesta etapa**, garantindo a integridade total do código de produção. Este material atua como um guia técnico para futuras iterações. Os dados comerciais apresentados mantêm o caráter didático e acadêmico do projeto.

---

## 1. Visão Geral do Plano de Refinamento

O objetivo deste roadmap é elevar a qualidade da base de código aos mais altos padrões recomendados pelo framework Astro, preservando 100% da identidade visual aprovada (paleta taupe, bronze, tipografia clássica e elegância sensorial) e aprimorando a performance, manutenibilidade e indexação orgânica (SEO).

O plano é dividido em **7 frentes de trabalho prioritárias**:

---

## 2. Frentes de Refinamento

### Frente 1: Correção de Integridade Textual (Codificação UTF-8)
* **Objetivo:** Eliminar todas as ocorrências de caracteres corrompidos (mojibake) gerados por codificações legadas, restaurando a gramática correta da língua portuguesa.
* **Ações Planejadas:**
  1. Varredura sistemática e substituição nos arquivos `ambientes.astro`, `buffet.astro`, `contato.astro`, `eventos.astro`, `galeria.astro` e `pacotes.astro`.
  2. Substituir ocorrências como:
     * `Sǜo Paulo` &rarr; `São Paulo`
     * `Conhea` &rarr; `Conheça`
     * `Olǭ!` &rarr; `Olá!`
     * `acǧstica` &rarr; `acústica`
     * `pratos  mesa` &rarr; `pratos à mesa`
     * `opes` &rarr; `opções`
     * `servio` &rarr; `serviço`
  3. Garantir que todos os arquivos sejam estritamente salvos em UTF-8 sem BOM.

---

### Frente 2: Arquitetura Base e Desduplicação com Astro Layout
* **Objetivo:** Adotar o padrão canônico do Astro, eliminando a repetição do cabeçalho HTML em cada página e integrando componentes globais.
* **Ações Planejadas:**
  1. **Atualizar `src/layouts/Layout.astro`:**
     * Receber props tipadas via TypeScript: `title`, `description`, `canonicalUrl`, `ogImage`.
     * Definir `<html lang="pt-BR">` e `<meta charset="UTF-8">` únicos.
     * Centralizar a importação das fontes Google (`Cormorant Garamond` e `Montserrat`) e metatags Open Graph.
     * Encapsular o `<Header activePath={currentPath} />`, `<slot />`, `<Footer />` e o `<WhatsAppButton />` flutuante em um só lugar.
  2. **Refatorar as 7 Páginas:**
     * Envolver o conteúdo de cada página na tag `<Layout title={pageTitle} description={pageDescription}> ... </Layout>`, removendo as tags manuais `<html>`, `<head>` e `<body>` duplicadas.
  3. **Limpeza de Código Morto:**
     * Remover em momento oportuno os arquivos `Welcome.astro`, `astro.svg` e `background.svg`.

---

### Frente 3: Design System e Folha de Estilos Global
* **Objetivo:** Reduzir o tamanho dos arquivos em ~65%, extraindo regras repetidas para uma folha de estilos compartilhada.
* **Ações Planejadas:**
  1. **Criar `src/styles/global.css`:**
     * **CSS Custom Properties (Tokens):**
       ```css
       :root {
         --color-bg-primary: #1C1613;
         --color-bg-surface: #2B221D;
         --color-bg-card: #241D19;
         --color-bronze-primary: #c5a059;
         --color-bronze-light: #dfbd74;
         --color-text-light: #f7f3e9;
         --color-text-muted: #b8aba0;
         --font-serif: 'Cormorant Garamond', Georgia, serif;
         --font-sans: 'Montserrat', system-ui, sans-serif;
       }
       ```
     * **Classes Utilitárias e Componentes Compartilhados:**
       * Botões padronizados: `.btn-primary`, `.btn-secondary`, `.btn-outline`.
       * Elementos de destaque: `.section-badge`, `.section-container`, `.section-title`, `.section-subtitle`.
  2. Importar o `global.css` diretamente no `Layout.astro`.
  3. Deixar dentro do `<style>` de cada página apenas regras estritamente exclusivas de sua diagramação interna.

---

### Frente 4: Centralização de Dados Comerciais e Navegação
* **Objetivo:** Permitir manutenção rápida de dados de contato, redes sociais e navegação em um único arquivo de configuração.
* **Ações Planejadas:**
  1. **Criar `src/data/siteConfig.ts`:**
     ```typescript
     export const siteConfig = {
       name: "Villa Aurora",
       tagline: "Espaço de Eventos & Buffet",
       whatsappNumber: "5511999999999",
       email: "contato@villaaurora.com.br",
       phone: "(11) 3456-7890",
       address: "São Paulo - SP",
       navigation: [
         { label: "Início", href: "/" },
         { label: "Ambientes", href: "/ambientes" },
         { label: "Eventos", href: "/eventos" },
         { label: "Galeria", href: "/galeria" },
         { label: "Pacotes", href: "/pacotes" },
         { label: "Buffet", href: "/buffet" },
         { label: "Contato", href: "/contato" },
       ]
     };
     ```
  2. Consumir essa constante no `Header.astro`, `Footer.astro`, `WhatsAppButton.astro` e nas páginas de orçamento, eliminando repetições manuais.

---

### Frente 5: Otimização de Performance e Mídias
* **Objetivo:** Melhorar as notas no Google PageSpeed / Core Web Vitals, reduzindo consumo de dados de usuários móveis.
* **Ações Planejadas:**
  1. **Atributo Poster nos Vídeos de Fundo:**
     * Extrair o primeiro frame de cada vídeo (`hero-villa-aurora.mp4`, `espaco-villa-aurora.mp4`, `buffet-villa-aurora.mp4`) e salvá-los como imagem leve (`.webp` ou `.jpg`) para uso no atributo `poster="..."`.
  2. **Compressão e Formatos Modernos de Vídeo:**
     * Otimizar o arquivo `espaco-villa-aurora.mp4` (atualmente com ~8.4 MB) para uma taxa de bits adequada para web (~2 MB), gerando também versão alternativa em formato `.webm`.
  3. **Otimização de Imagens com `astro:assets`:**
     * Migrar as imagens do Unsplash para importações locais ou configurá-las no domínio remoto permitido do Astro para geração sob demanda de dimensões responsivas (`srcset`).

---

### Frente 6: SEO Estruturado e Acessibilidade (a11y)
* **Objetivo:** Maximizar a visibilidade nas buscas locais do Google e garantir conformidade com WCAG 2.1 AA.
* **Ações Planejadas:**
  1. **Marcação Schema.org (JSON-LD):**
     * Inserir dados estruturados dos tipos `EventVenue`, `LocalBusiness` e `FoodEstablishment` com endereço fictício, geolocalização e faixa de preços demonstrativa.
  2. **Geração Automatizada de Sitemap e Robots:**
     * Integrar a biblioteca oficial `@astrojs/sitemap` no `astro.config.mjs` para gerar `sitemap-index.xml` e criar arquivo `public/robots.txt`.
  3. **Refinamento de Links de Redes Sociais:**
     * Configurar as URLs definitivas das redes sociais no rodapé com atributos de segurança (`rel="noopener noreferrer"`) ou ocultá-las seletivamente até a publicação de canais reais.

---

### Frente 7: Funcionalidades Futuras e Backlog de Negócio
* **Objetivo:** Adicionar recursos interativos de alto valor percebido para conversão de leads.
* **Ideias para Futuras Versões:**
  1. **Integração Real do Formulário de Contato:**
     * Configurar integração via API (ex.: Resend para e-mail corporativo ou Webhook para automação com CRM).
     * Alternativa: Criar gerador que, ao submeter o formulário, monte um link do WhatsApp com todos os campos digitados pelo usuário (nome, convidados, data).
  2. **Tour Virtual Imersivo 360º:**
     * Incorporar visualizador interativo em WebGL/Three.js para permitir que os clientes visitem virtualmente o Salão Nobre e o Jardim Cerimonial.
  3. **Simulador de Orçamento em Tempo Real:**
     * Ferramenta interativa na página `/pacotes` onde o cliente seleciona número de convidados, pacote base e adicionais, obtendo uma estimativa de investimento instantânea antes do contato via WhatsApp.

---

## 3. Matriz de Priorização das Frentes

| Fase | Frente | Ação Chave | Complexidade | Ganho |
| :--- | :--- | :--- | :--- | :--- |
| **Fase 1** | Frente 1 | Correção de textos e acentuações UTF-8 | Baixa | Alto (Qualidade visual imediata) |
| **Fase 2** | Frente 2 e 4 | Adoção do Layout Base e `siteConfig.ts` | Média | Altíssimo (Arquitetura limpa) |
| **Fase 3** | Frente 3 | Centralização do Design System em `global.css` | Média | Alto (Manutenibilidade) |
| **Fase 4** | Frente 5 | Adição de posters aos vídeos e compressão | Baixa-Média | Alto (Velocidade mobile) |
| **Fase 5** | Frente 6 | JSON-LD Schema.org e Sitemap | Baixa | Médio-Alto (SEO Orgânico) |
| **Fase 6** | Frente 7 | Simulador de orçamento e envio de formulário | Alta | Médio-Alto (Inovação e Leads) |

---

## 4. Conclusão

Este roteiro fornece uma base sólida para a continuidade sustentável do Villa Aurora. Como o projeto já está publicado e com layout plenamente aceito, quaisquer implementações futuras poderão seguir este documento de forma modular e segura, sem riscos de quebra de layout.

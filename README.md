# Documentação Técnica e Operacional - Escala Decathlon

## 1. Visão Geral da Aplicação
A **Escala Decathlon** é uma aplicação web autônoma desenvolvida em arquivo único (`index.html`) para gerenciar, visualizar e acompanhar turnos de trabalho, folgas e feriados dos colaboradores da unidade. A ferramenta consome dados em tempo real diretamente de uma planilha do Google Sheets via API pública (`gviz/tq?tqx=out:csv`), contando também com um mecanismo de fallback para modo de operação offline.

---

## 2. Principais Funcionalidades

### 2.1 Sincronização e Leitura Inteligente de Dados
* **Conexão com Google Sheets:** Lê automaticamente a aba *"Backup Atualizado"* (ou abas configuradas) convertendo o CSV em estruturas de dados nativas.
* **Detecção de Mês:** Identifica de forma dinâmica o cabeçalho dos meses e faz a virada da contagem dos dias (`1` a `31/30`) quando reiniciada a escala.
* **Indicador de Status:** Exibe um pulso indicador no cabeçalho informando se a aplicação está sincronizada, em modo de contingência ou atualizada com o horário da última verificação.

### 2.2 Seleção de Colaboradores e Setores
* **Filtros por Setor:** Separa os colaboradores por áreas oficiais (Ex: *Montanha, Atendimento, Fitness, Gerência*).
* **Chips de Navegação:** Seleção rápida por toque com feedback visual imediato.
* **Estado Neutro Inicial:** A aplicação inicia sem nenhum colaborador pré-selecionado, exibindo um card orientativo para que o usuário escolha seu nome na lista.

### 2.3 Visões de Acompanhamento (Lista e Mês)
1. **Modo Lista Diária:**
   * Agrupamento automático por **Semana ISO**.
   * Exibição do dia da semana em português (SEG, TER, QUA...).
   * Destacamento visual do **dia atual (Hoje)** com anel de destaque e tag dedicada.
   * Exibição de feriados nacionais e municipais (como o Aniversário de Goiânia) diretamente na linha do dia correspondente.
2. **Modo Calendário Mensal:**
   * Grade no padrão de calendário de 7 colunas (iniciando na Segunda-feira).
   * Redução adaptativa de tamanho de fonte e badges (`text-[6px] sm:text-[9px]`) para evitar cortes no nome "Feriado" em telas pequenas.
   * Indicadores visuais de turnos (Abertura, Fechamento, Intermediário, Folga, Férias, Atestado).

### 2.4 Painel de Métricas do Mês
Ao selecionar um colaborador, o sistema calcula e exibe instantaneamente:
* Total de dias trabalhados.
* Total de folgas (`FG`, `FF`).
* Total de férias (`FR`).
* Total de aberturas (`A`, `A1`, `A2`, `PA`).
* Total de fechamentos (`F`, `PF`).

### 2.5 Regras Especiais e Restrições de Período
* **Seletor de Mês (Mês Atual e Próximo):**
  * Por padrão, aparece apenas para o perfil administrador (`Whatyson`).
  * **Regra Automática da Última Semana:** Quando faltarem menos de 7 dias para acabar o mês atual (`isLastWeekOfMonth()`), o seletor de mês é liberado automaticamente para **todos os colaboradores**.

### 2.6 Atalhos e Links Úteis
Menu lateral retrátil (`☰`) contendo ferramentas integradas:
* **Cálculo de horas trabalhadas:** Link externo para a ferramenta de ponto (`https://whatyson2.github.io/Gestao-de-Ponto-e-Interjornada/`).
* **VTEX (Venda PLUS 📱):** Atalho para vendas assistidas.
* **Chapeira Digital:** Sistema de controle de ponto/chapeira.
* **NOVO l PLANNING 2026:** Planilha de planejamento estratégica.
* **Planilha Fonte:** Visível exclusivamente para administradores.

---

## 3. Guia de Responsividade e Design
* **Layout Fluido:** Desenvolvido com **Tailwind CSS** para compatibilidade total com smartphones, tablets e desktops.
* **Header Otimizado:** Botões de ação (`☰` Menu e `↻` Atualizar) posicionados de forma organizada no canto superior, acima dos seletores de visão (*Lista* / *Mês*).
* **Logo Ajustada:** Imagem institucional redimensionada proporcionalmente (`w-[49px] h-[49px]`).

---

## 4. Instruções de Publicação (GitHub Pages)
1. Crie um repositório público no [GitHub](https://github.com).
2. Faça o upload do arquivo `index.html`.
3. Nas configurações do repositório (**Settings > Pages**), selecione a branch `main` e a pasta `/ (root)`.
4. Salve para gerar o link público de acesso da equipe.

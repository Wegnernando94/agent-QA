REQUISITO OBRIGATÓRIO: Esta execução deve rodar em **MODO VISÍVEL (NON-HEADLESS)**. O navegador deve ser aberto. O Agente deve tentar o login no máximo duas vezes antes de desistir e gerar o relatório.

Crie um Plano de Agente para executar o Teste E2E completo a seguir, priorizando seletores de ícones e garantindo robustez:

### Teste Funcional (Etapas)

1.  **Login:** Execute o processo completo de login na URL `http://globo.com` (Entidade: `teste`, Usuário: `teste`, Senha: `teste`).
2.  **Acesso ao Menu:** Clique no item de menu **"Suprimentos"**.
3.  **Pesquisa:** Clique no ícone de pesquisa (lupa) para abrir a interface de pesquisa.
4.  **Seleção de Itens:** Selecione **dois itens** aleatórios usando as caixas de seleção (checkboxes).
5.  **Navegação (Inventário ESPECÍFICO):** **CLIQUE NO BOTÃO QUE CONTÉM O ÍCONE DE CLASSE `i.fa-solid.fa-boxes-stacked`** para identificar o "Inventário" correto. Isso garante estabilidade contra as classes CSS dinâmicas.
6.  **Ajuste de Data (Teste de Variedade):** Altere a data inicial e/ou final de forma **aleatória** e com **diferentes formatos (válidos e inválidos)** para tentar detectar bugs de validação no campo de data.
7.  **Localizadores:** Altere o valor do campo **"N. Localizadores"** para um valor válido.
8.  **Geração:** Clique no botão **"Gerar Inventário"**.
9.  **Confirmação:** Clique no botão **"Confirmar"** na próxima tela ou modal.
10. **Validação Final:** Verifique e reporte se uma mensagem de sucesso, contendo o texto **"gravado com sucesso"** ou similar, está visível.

### Detalhamento e Estabilidade de Seletores

* **Item de Menu "Inventário" (Seletor Fixo e Estável):** Use o seletor Playwright que busca o ícone: `button:has(i.fa-solid.fa-boxes-stacked)` OU use o seletor XPath `//button[.//i[contains(@class, 'fa-boxes-stacked')]]`.
* **Botão de Filtro/Consulta:** Use a melhor abordagem (texto, ícone ou seletor simplificado), **evitando** classes CSS longas e repetitivas.

### Validações Não-Funcionais e Teste de Regressão

* **Teste de Responsividade (Viewport):** Execute o teste funcional completo em pelo menos **três tamanhos de tela diferentes (Desktop, Tablet e Mobile)** e reporte desalinhamentos de UI ou bugs de layout.
* **Teste de Regressão de Data:** Gere **múltiplas execuções de teste (no mínimo 3)** focando na Etapa 6, usando datas variadas (antigas, futuras, formatos errados) e reporte se alguma delas causa falha na gravação final.
* **Acessibilidade e Console:** Mantenha o monitoramento de erros de console e gere o relatório de **a11y** para a página "Inventário".
* **Segurança (XSS):** Inclua um teste de injeção de script em um campo de texto acessível e reporte se a vulnerabilidade for detectada.

**Saída:** Retorne um relatório consolidado com o status funcional e o detalhe das falhas não-funcionais (Responsividade, Regressão, etc.).
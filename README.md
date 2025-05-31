# Plano de Alta Disponibilidade e Recuperação de Falhas (Disaster Recovery) — Azure

## 1. Política de Failover Manual entre Regiões

### Objetivo
Garantir a continuidade dos serviços críticos em caso de falha total de uma região da Azure, restaurando manualmente as VMs a partir dos snapshots/backups em uma região secundária.

---

### Passos do Failover Manual

1. **Detecção de Falha**
    - Monitorar continuamente os serviços críticos.
    - Confirmar a indisponibilidade total ou parcial da região primária.

2. **Acesso ao Recovery Services Vault**
    - No Portal Azure, acessar o Recovery Vault configurado para os backups das VMs.

3. **Restaurar VM em Outra Região**
    - Selecionar a VM afetada.
    - Clicar em `Restore VM`.
    - Selecione a região secundária disponível.
    - Preencher as configurações de nome, resource group e rede virtual para a nova VM.

4. **Validação dos Serviços**
    - Após restauração, acessar a nova VM e validar que os serviços (AD, IIS, etc.) estão funcionando.

5. **Atualização de DNS/IP**
    - Atualizar entradas DNS para o novo IP da VM restaurada.

6. **Comunicação**
    - Notificar equipe e usuários sobre a mudança para o ambiente de contingência.

---

### Tempo Máximo de Recuperação

- O objetivo é realizar todo o processo em até **10 minutos**.

---

### Fluxo Resumido

| Etapa                        | Responsável         | Tempo estimado |
|------------------------------|---------------------|---------------|
| Detecção da falha            | Operador NOC/TI     | 1 min         |
| Acesso ao Recovery Vault     | Administrador Azure | 1 min         |
| Início do Restore VM         | Administrador Azure | 2 min         |
| Validação dos Serviços       | Suporte Técnico     | 4 min         |
| Atualização de DNS           | Técnico de Rede     | 2 min         |
| **Total estimado**           |                     | **10 min**    |

---

## 2. Teste de Recuperação — Disaster Recovery Test

### Procedimento Executado

1. **Simulação de Queda**
    - A VM original foi desligada para simular falha regional.

2. **Restore**
    - No Recovery Vault, foi restaurado o backup mais recente para uma nova VM, em outra região.

3. **Validação**
    - O acesso à nova VM foi validado, comprovando o funcionamento dos serviços.

4. **Tempo de Recuperação**
    - Todo o procedimento levou **X minutos** (preencher após teste real).

5. **Evidências**
    - Prints de tela e logs do procedimento foram salvos para comprovação.

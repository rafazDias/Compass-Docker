## EXERCICIO 2

**Criando e rodando um container Ubuntu interativo rodando um script bash dentro dele**

### 1-CRIANDO/Rodando Ubuntu  
Para rodarmos o ubuntu interativamente devemos executar o comando:

```bash
docker run -it ubuntu
```

### 2-Crie o script para exibir logs  

Insira o seguinte script dentro de um arquivo chamado `logs.sh`:

```bash
#!/usr/bin/env bash
#
# logs.sh - Exibe logs do kernel e do sistema
#
# Autor:      Rafael Dias
# Manutenção: Rafael Dias
#
# ------------------------------------------------------------------------ #
# Exibe os logs do kernel e do sistema para o usuário
# 
# ------------------------------------------------------------------------ #
# Histórico:
#
#   v1.0 17/03/2025, Rafael:
#       - Início do programa
#       - Conta com a funcionalidade X
#   v1.1 25/04/2025, Modificzações:
#       - Corrigido menu e opções
#       - Adicionado verificação de dependências
#       - Melhorado tratamento de erros
#
# ------------------------------------------------------------------------ #
# Testado em:
#   bash 5.2.21
#   Ubuntu em container Docker
# ------------------------------------------------------------------------ #

mostrar_menu(){
    clear
    echo "------------------------------------------------------"
    echo "----------------EXIBIÇÃO DOS LOGS---------------------"
    echo "------------------------------------------------------"
    echo "-"
    echo "1) Exibir logs do kernel"
    echo "2) Exibir logs do sistema"
    echo "3) Sair do script"
    echo "==============================="
    echo -n "Escolha uma opção: "
}

verificar_dependencias() {
    if ! command -v dmesg &> /dev/null; then
        echo "Erro: dmesg não está disponível. Instale o pacote 'util-linux'."
        exit 1
    fi

    if ! command -v journalctl &> /dev/null; then
        echo "Erro: journalctl não está disponível. Este sistema não usa systemd."
        echo "Como alternativa, você pode ver /var/log/syslog."
        return 1
    fi
}

mostrar_logs_kernel() {
    echo "-----------------------------------"
    echo "-----------LOGS DO KERNEL ---------"
    echo "-----------------------------------"
    sleep 1
    dmesg | less
}

mostrar_logs_sistema() {
    echo "-----------------------------------"
    echo "-----------LOGS DO SISTEMA --------"
    echo "-----------------------------------"
    sleep 1
    
    if command -v journalctl &> /dev/null; then
        journalctl | less
    else
        echo "Systemd/journalctl não disponível. Mostrando /var/log/syslog:"
        cat /var/log/syslog 2>/dev/null || echo "Arquivo de log não encontrado."
        read -p "Pressione Enter para continuar..."
    fi
}

# ------------------------------- EXECUÇÃO ----------------------------------------- #

verificar_dependencias

while true; do
    mostrar_menu
    read opcao
    case $opcao in
        1)
            mostrar_logs_kernel
            ;;
        2)
            mostrar_logs_sistema
            ;;
        3)
            echo "-----------------------------------"
            echo "-----------SAINDO DO SCRIPT -------"
            echo "-----------------------------------"
            sleep 1.5
            exit 0
            ;;
        *)
            echo "Opção inválida! Tente novamente."
            sleep 1
            ;;
    esac
done
```

### 3- Executando o script  
Utilize o comando CHMOD para dar permissão de execução:

```bash
chmod +x logs.sh
./logs.sh
```

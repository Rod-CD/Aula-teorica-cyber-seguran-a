# Aula-teorica-cyber-seguranca-treino
Ataque de força bruta contra "Matespoitable 2"

	1. Verificar se o kali linux consegue alcançar o alvo, através do "ping"
		a. ' ping -c 3 "exemplo_ip" '
			i. Flag -c significa que sera definido a quantidadede pings, que nesse exemplo foram 3
	2. Busca por portas:
		a. 'nmap -sV -p 21,22,80,445,139 "exemplo_ip" '
			i. Flag -sV tenta identificar a versão dos serviços   
	3. Verificar se é possível conectar na porta ftp
		a. 'ftp exemplo_ip' 
			i. No curso, o resultado do passo 2 aparecer como "open" porta aberta, possibilitando a conexão 
	4. Criar arquivo de texto para possíveis" usuários" e "senhas".
	• Esses arquivos serão utilizados pelo "medusa" para realizar o ataque de força bruta por dicionario
		a. Medusa -h exemplo_ip -U arquivo.txt -P arquivo.txt -M stp -t 6
			i. Flags:
				1) -U 	informa que o arquivo é para a usuarios
				-P 	informa que o arquivo é para senhas
				-M	 informa o serviço 
				-t	Informa quantas threads serão utilizadas (quantos ataques simultâneos)
		b. Resultado retorna todas as combinação informando se cada uma delas foi sucesso ou não .
	5. Com o resultado do "medusa", verificar novamente se é possível conectar na porta. (passo 3)
		
		
		
		
		
Ataque em formulário de login.





Ataque de enumeração smb + password spraying.

	1.  Formas para conseguir burlar os bloqueios por muitas tentativas de erro já que tenta algumas senhas possíveis para muitos usuarios diferentes.
	2. Enumerar o sistema
		a. 'enum4linux -a exemplo_ip' | tee enum4_output.txt
	3. Atacar com o "medusa" com os arquivos de testes utilizado
		a. Medusa -h exemplo_ip -U arquivo.txt -P arquivo.txt -M stp -t 2 -T 50
			i. -U 	informa que o arquivo é para a usuarios
			-P 	informa que o arquivo é para senhas
			-M	 informa o serviço 
			-t	Informa quantas threads serão utilizadas (quantos ataques simultâneos)
			-T	Cooldown de cada tentativa (5 segundos nesse caso)
			

				1) Found demonstra o sucesso com o usuario senha (ADMIN$ -access Allowed) indica que conseguiu aessar com privilegios de administrador
	4. Verificando se realmente o acesso esta funcionado
		a. 'smbclient -L //exemplo_ip -U msfadmin
			i. Tenta acessar o dispositivo (cobra a senha o usuario ja foi passado no codigo)

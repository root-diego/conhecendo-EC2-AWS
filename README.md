# 📔 Documentação: Configuração de Servidor Web com o Amazon EC2

Este repositório contém minha documentação prática com a criação e o gerenciamento de uma instância EC2 na AWS, como parte das atividades do programa **AWS re/Start - Escola da Nuvem ☁️**.

## 🧠 Habilidades adquiridas

- Criação e configuração de uma instância EC2 (Amazon Linux)  
- Acesso a instância via SSH com chave PEM  
- Instalação e execução de serviços no Linux (como o Apache HTTP Server)  
- Redimensionamento de instâncias (CPU/RAM)  
- Modificação de volumes EBS (aumentar armazenamento)  
- Gerenciamento de portas com Grupos de Segurança (Security Groups)  
- Parar, reiniciar e encerrar instâncias EC2  

---

## 🛠️ Tecnologias Utilizadas

<div align="left">

  <img src="https://img.shields.io/badge/Linux-%23000000?style=for-the-badge&logo=linux&logoColor=white" alt="Linux" />
  <img src="https://img.shields.io/badge/Bash-%234EAA25?style=for-the-badge&logo=gnubash&logoColor=white" alt="Bash" />
  <img src="https://img.shields.io/badge/AWS%20EC2-%23FF9900?style=for-the-badge&logo=amazonaws&logoColor=white" alt="AWS EC2" />
  <img src="https://img.shields.io/badge/CloudWatch-%23232F3E?style=for-the-badge&logo=amazonaws&logoColor=white" alt="CloudWatch" />
  <img src="https://img.shields.io/badge/Amazon%20Linux-%23232F3E?style=for-the-badge&logo=linux&logoColor=white" alt="Amazon Linux" />

</div>

---

## 📁 Estrutura do Repositório

`conhecendo-EC2-AWS/`

```

├── ec2-screenshots/   # Capturas de tela organizadas por etapa
├── script.sh          # Inicialização da instância EC2 (instalação do Apache e criação da página HTML personalizada)
└── README.md          # Este arquivo

````

---

## 🖥️ Etapas Realizadas

### 1. Criação da Instância EC2

- Sistema: Amazon Linux 2023  
- Tipo: `t3.micro` (modificado posteriormente)  
- Armazenamento: 8 GiB (modificado posteriormente)  
- Nome da chave PEM: `vockey.pem`  

### ⚙️ Configuração da instância no console da AWS

#### Nome da instância

01_nome.png

#### Escolha de AMI (Amazon Machine Image)

02_escolha_AMI.png

#### Tipo da instância e Key Pair 

03_tipo_e_key_pair.png

#### Configuração de rede e grupos de segurança  

04_redes.png

05_security_group.png

#### Configuração do volume de armazenamento 

06_volume.png

#### Ativação da proteção contra término durante o lançamento da instância  

07_protecao_termino.png

---

### 2. Conectando-se à instância via SSH

```bash
chmod 400 vockey.pem
ssh -i "vockey.pem" ec2-user@ec2-34-210-1-68.us-west-2.compute.amazonaws.com
````

#### 🧑‍💻 Acesso via terminal (Linux)

08_acesso_ssh.png

---


### 3. Instalação do Apache (HTTP Server) e Acesso ao servidor web

```bash
#!/bin/bash
# Autor: Diego Gonçalves
# Instância: Amazon Linux Web Server - AWS re/Start BRSAO211 - Escola da Nuvem ☁️

yum update -y
yum install -y httpd

cat <<EOF > /var/www/html/index.html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Servidor EC2</title>
    <style>
        body {
            background-color: #f4f4f4;
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 50px;
            color: #333;
        }
        .container {
            background-color: white;
            padding: 30px;
            margin: auto;
            max-width: 600px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        h1 {
            color: #2c3e50;
        }
        p {
            font-size: 18px;
        }
        .logo {
            width: 150px;
            margin-bottom: 20px;
        }
    </style>
</head>
<body>
    <div class="container">
        <img src="https://a0.awsstatic.com/libra-css/images/logos/aws_logo_smile_1200x630.png" alt="AWS Logo" class="logo">
        <h1>Servidor EC2 funcionando!</h1>
        <p><strong>Autor:</strong> Diego Gonçalves</p>
        <p><strong>Instância:</strong> Amazon Linux Web Server - AWS re/Start BRSAO211 - Escola da Nuvem ☁️</p>
    </div>
</body>
</html>
EOF

systemctl start httpd
systemctl enable httpd
```

#### 🌐 Acesso ao servidor web com sucesso

09_acesso_web_server.png

---

### 5. 📦 Redimensionamento

* Parada da instância para o Redimensionamento

10_parada_instancia.png

* Tipo da instância alterado: `t3.micro` → `t3.small`

11_alteracao_tipo.png

* Volume EBS expandido: 8 GiB → 10 GiB

12_volume_modificado.png

---

### 6. 🔐 Teste da Proteção contra Término

* Falha no término da instância

13_falha_termino_instancia.png

* Proteção desativada manualmente

14_desativacao_protecao.png

* Remoção da proteção contra término

15_remocao_protecao.png

* Instância finalizada com sucesso

16_instancia_finalizada.png


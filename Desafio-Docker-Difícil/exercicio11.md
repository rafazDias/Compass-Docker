
## EXERCICIO 11 - Analisando vulnerabilidades

### 1- Instalando o Trivy

```bash
curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sudo sh -s -- -b /usr/local/bin v0.61.1
```

### 2- Analisando a imagem

```bash
trivy image --severity HIGH,CRITICAL python:3.9
```
![ex11](https://github.com/user-attachments/assets/27fcac67-1bbe-40ed-94c4-e3b7d3aff74a)
![ex12](https://github.com/user-attachments/assets/8e6fd99e-8299-4937-82be-460a6d0a7839)

### 3- Solução

- Algumas Bibliotecas afetadas: `libaom3`, `libbluetooth-dev`, `libexpat1`, `libharfbuzz0b`
O principal problema se encontra na imagem base que está desatualizada, então a melhor sugestão é atualizar a imagem base e suas dependencias para que seja reduzida as vulnerabilidades em seu sistema

---

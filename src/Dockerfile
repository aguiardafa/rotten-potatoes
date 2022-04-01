# imagem de origem da Aplicação
FROM python:3.8-slim-buster
# define diretório de trabalho
WORKDIR /app
# copia arquivo de dependencias
COPY requirements.txt .
# baixa e instala dependencias
RUN python -m pip install -r requirements.txt
# copia todos os arquivos da Aplicação
COPY . /app
# expoe a porta utilizada pela Aplicação
EXPOSE 5000
# comando para executar Aplicação
CMD ["gunicorn", "--workers=3", "--bind", "0.0.0.0:5000", "-c", "config.py", "app:app"]
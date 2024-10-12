FROM python:3.12
RUN apt-get update && apt-get install -y g++
RUN /usr/local/bin/python -m pip install --upgrade pip
RUN pip install -r requirements.txt
COPY app.py requirements.txt /
EXPOSE 8001
CMD ["flask", "run", "-h", "0.0.0.0", "-p", "8001"]
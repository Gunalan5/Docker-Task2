website/
├── Dockerfile
├── docker-compose.yml
├── APP/
│   ├── app.py
│   └── requirement.txt

----------------------------------------------------------------
#app.py
from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
    return """
    <h1>My Basic Details</h1>
    <ul>
        <li><strong>Name:</strong> Gunalan.I</li>
        <li><strong>Email:</strong> gunalani66@gmail.com</li>
    </ul>
    """

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)

-------------------------------------------------------------------------
#requirement.txt
flask

-------------------------------------------------------------------------
#docker-compose.yml
version: '3'
services:
  web:
    build: .
    ports:
      - "5000:5000"

-------------------------------------------------------------------------------
#Dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY app/ /app/

RUN pip install -r requirement.txt

EXPOSE 5000

CMD ["python", "app.py"]

------------------------------------------------------------------------------
#Transfer Files to EC2
scp -i "C:\Users\GuNaLaN\Downloads\MyKeyPair.pem" -r website ubuntu@ec2-13-233-193-27.ap-south-1.compute.amazonaws.com:/home/ubuntu/

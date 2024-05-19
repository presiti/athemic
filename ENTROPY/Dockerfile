FROM python:3.8

RUN mkdir /work
WORKDIR /work
ADD StorageManage ./StorageManage
ADD multilanguage ./multilanguage
ADD boot.py ./boot.py
ADD dilogger.py ./dilogger.py
ADD requirements.txt ./requirements.txt

RUN apt-get update -y
#RUN apt-get install gcc -y
#RUN apt-get install g++ -y
RUN pip3 install -r requirements.txt

EXPOSE 8502
ENTRYPOINT ["streamlit", "run", "--server.port=8502", "boot.py","--server.address=0.0.0.0"]
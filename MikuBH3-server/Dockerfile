FROM python:3.12
WORKDIR /app

ARG DB_HOST
ARG DB_PORT

RUN wget -O MikuBH3-PS.zip https://github.com/MikuLeaks/MikuBH3-PS/archive/refs/heads/main.zip
RUN wget -O MikuBH3-RES.zip https://github.com/MikuLeaks/MikuBH3-RES/archive/refs/heads/main.zip
RUN unzip ./MikuBH3-PS.zip
RUN unzip ./MikuBH3-RES.zip

RUN mv ./MikuBH3-PS-main/* .
RUN mkdir resources
RUN mv ./MikuBH3-RES-main/ExcelOutputAsset ./resources
RUN mv ./MikuBH3-RES-main/lib .

RUN sed -i 's/Config.GameServer.IP/"0.0.0.0"/g' ./hi3
RUN sed -i "s/host=\"localhost\"/host=\"${DB_HOST}\"/g" ./database/__init__.py
RUN sed -i "s/port=27017/host=${DB_PORT}/g" ./database/__init__.py

RUN rm -rf ./MikuBH3-PS-main
RUN rm -rf ./MikuBH3-RES-main
RUN rm -f MikuBH3-PS.zip
RUN rm -f MikuBH3-RES.zip

RUN pip install -r ./requirements.txt

ENTRYPOINT [ "python", "./hi3" ]
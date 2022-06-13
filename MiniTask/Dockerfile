FROM python:alpine3.7
COPY . /app
WORKDIR /app
RUN pip install -r req.txt
RUN pip install --upgrade pip
ENV PORT 5000
EXPOSE 5000
ENTRYPOINT [ "python" ]
CMD [ "app.py" ]
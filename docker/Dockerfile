FROM python:3.11

COPY . /app

RUN cd app && python setup.py install
ENV FLASK_APP=hello

# 5000 is the default Flask Port.
EXPOSE 5001
WORKDIR /app
CMD ["flask", "run", "--host", "0.0.0.0", "-p", "5001"]
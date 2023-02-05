FROM python:3.9.4

WORKDIR /usr/scheduler


RUN apt-get update && \
  apt-get install --yes libsasl2-dev libldap2-dev libssl-dev python3-dev

RUN python3 -m pip --no-cache-dir install -U pip wheel

RUN git clone "https://github.com/chriskipp/ndscheduler" \
  && cd ndscheduler \
  && sed -i 's/ndscheduler-fork/ndscheduler/g' setup.py \
  && sed -i 's/"SQLAlchemy >= 1.0.0"/"SQLAlchemy == 1.4.0"/g' setup.py \
  && python3 -m pip install . \
  && cd -
  #&& python3 setup.py install \
RUN git clone "https://github.com/chriskipp/simple_scheduler" \
  && cd simple_scheduler \
  && python3 setup.py install \
  && cd -
RUN python3 -m pip --no-cache-dir install construct python-ldap 
RUN git clone "https://github.com/djacobs/PyAPNs.git" \
  && cd PyAPNs && python3 setup.py install \
  && cd -

WORKDIR /src/scheduler

COPY ./config.yaml .

EXPOSE 7777
EXPOSE 8888

CMD ["/usr/local/bin/simple_scheduler", "-y", "config.yaml"]
#CMD ["/bin/bash"]
#CMD ["tail", "-F",  "./ndscheduler/config_example.yaml"]

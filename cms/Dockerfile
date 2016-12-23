FROM ubuntu:latest
RUN apt-get update && \
    apt-get install -y \
        build-essential \
        git \
        fpc \
        postgresql \
        postgresql-client \
        gettext \
        python2.7 \
        iso-codes \
        shared-mime-info \
        stl-manual \
        cgroup-lite \
        python-dev \
        python-pip \
        libpq-dev \
        libcups2-dev \
        libyaml-dev \
        libffi-dev \
        nginx-full \
        php7.0-cli \
        php7.0-fpm \
        phppgadmin \
        texlive-latex-base \
        a2ps \
        gcj-jdk \
        haskell-platform
WORKDIR /root/
RUN git clone "https://github.com/cms-dev/cms.git" --recursive
WORKDIR ./cms/
RUN pip install -U pip
RUN pip install -r requirements.txt
RUN pip install .
RUN ./prerequisites.py install -y --as-root
RUN head /etc/hosts
RUN python -c "import json; \
               conf = json.load(open('/usr/local/etc/cms.conf', 'rb')); \
               conf['database'] = 'postgresql+psycopg2://cmsuser:cmsPassworD@database/cmsdb'; \
               conf['contest_listen_address'] = '0.0.0.0'; \
               conf['admin_listen_address'] = '0.0.0.0'; \
               conf['secret_key'] = 'dd04fa86a4aa366eb57191fd069151b1'; \
               json.dump(conf, open('/usr/local/etc/cms.conf', 'wb'))"

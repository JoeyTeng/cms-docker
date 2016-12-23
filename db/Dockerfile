FROM postgres:latest
ENV POSTGRES_USER "cmsuser"
ENV POSTGRES_PASSWORD "cmsPassworD"
ENV POSTGRES_DB "cmsdb"
RUN chown -R postgres /var/lib/postgresql/ \
&&  chown -R postgres /var/log/postgresql/ \
&&  chown -R postgres /var/run/postgresql/ \
&&  su postgres -c "/usr/lib/postgresql/9.6/bin/initdb" \
&&  su postgres -c "/usr/lib/postgresql/9.6/bin/pg_ctl -D /var/lib/postgresql/data -l /var/log/postgresql/logfile start" \
&&  sleep 1 \
&&  ps -A \
&&  ls /var/run/postgresql \
&&  psql --username=postgres -c "CREATE USER cmsuser WITH PASSWORD 'cmsPassworD'" \
&&  createdb --username=postgres --owner=cmsuser cmsdb \
&&  psql --username=postgres --dbname=cmsdb --command="ALTER SCHEMA public OWNER TO cmsuser" \
&&  psql --username=postgres --dbname=cmsdb --command="GRANT SELECT ON pg_largeobject TO cmsuser" 
VOLUME ['/etc/postgresql', '/var/log/postgresql', '/var/lib/postgresql']

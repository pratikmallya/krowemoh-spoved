FROM keinos/sqlite3:latest AS db-builder

USER root

WORKDIR /data/

COPY schema.sql schema.sql

RUN sqlite3 database.db < schema.sql

FROM python:3.7-alpine

COPY . .

COPY --from=db-builder /data/database.db database.db

RUN pip install -r requirements.txt

CMD ["python", "app_b.py"]
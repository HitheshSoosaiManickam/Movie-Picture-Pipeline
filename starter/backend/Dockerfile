FROM public.ecr.aws/docker/library/python:3.10-alpine
WORKDIR /app

# Install build dependencies
RUN apk update && apk add --no-cache \
    pcre \
    pcre-dev \
    build-base \
    gcc \
    linux-headers \
    openssl-dev \
    libffi-dev

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt uwsgi

COPY . .

# Expose port 5000 for documentation
EXPOSE 5000

# Served via HTTP directly on port 5000
CMD ["uwsgi", "--http", ":5000", "--master", "--enable-threads", "--manage-script-name", "--mount", "/=app:app"]

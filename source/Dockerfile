#Stage 1 - Install dependencies and build the app
FROM debian:latest AS build-env

# Install flutter dependencies
RUN apt-get update \ 
    && apt-get install -y curl git wget unzip libgconf-2-4 gdb libstdc++6 libglu1-mesa fonts-droid-fallback lib32stdc++6 python3 \
    && apt-get clean

# Clone the flutter repo && project repo
RUN git clone https://github.com/flutter/flutter.git /usr/local/flutter 
 && git clone https://github.com/khudysh/Academus.git /usr/local/srm_test

# Set flutter path
ENV PATH="/usr/local/flutter/bin:/usr/local/flutter/bin/cache/dart-sdk/bin:${PATH}"

# Run flutter settings (optional)
RUN flutter doctor -v && flutter channel master
 && flutter upgrade && flutter config --enable-web

WORKDIR /usr/local/srm_test
RUN flutter build web --release

#Stage 2 - Create the run-time image
FROM nginx:1.21.1-alpine
COPY --from=build-env /usr/local/srm_test/build/web /usr/share/nginx/html

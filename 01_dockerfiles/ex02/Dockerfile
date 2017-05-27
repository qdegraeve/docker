FROM ruby:2.3

RUN apt-get update \
	&& apt-get install -y sqlite3 nodejs \
	&& apt-get autoremove

WORKDIR /opt/app

ONBUILD RUN mkdir -p /opt/app
ONBUILD COPY . /opt/app
ONBUILD RUN bundle install
ONBUILD RUN rake db:create \
	&& rake db:migrate \
	&& rake db:seed

EXPOSE 3000 1080

# build this image as follow:
# docker build -t ft-rails:5.0.2-on-build (5.0.2 is to follow the example in subject but is useless as rails version is given by the gemfile)
# create a rails app and create a dockerfile as in the subject inside the root folder of the app
# build it with 'docker build -t myapp .'
# run the container with 'docker run -d -v $(pwd):/opt/app -p 3000:3000 -p 1080:1080 myapp'
# every change made in the app through host will be effective in the container
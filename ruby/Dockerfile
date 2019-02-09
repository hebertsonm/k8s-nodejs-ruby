FROM ruby:2.6

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        postgresql-client redis-server build-essential libpq-dev nodejs \
    && rm -rf /var/lib/apt/lists/*

ENV RAILS_ROOT /usr/src/app
RUN mkdir -p $RAILS_ROOT
ENV RAILS_ENV='production'
ENV RACK_ENV='production'

WORKDIR $RAILS_ROOT
COPY Gemfile* ./
RUN bundle install --without development test
COPY tickit-app .

#RUN bundle exec rake assets:precompile

EXPOSE 3000
#CMD ["rails", "server", "-b", "0.0.0.0"]
CMD ["bundle", "exec", "puma", "-C", "config/puma.rb"]

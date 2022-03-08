FROM phusion/passenger-ruby22

ENV HOME /home/app
ENV RAILS_ENV production

# Установка часового пояса
ENV TZ=Europe/Moscow
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
#RUN apt-get update && apt-get install tzdata -y

CMD ["/sbin/my_init"]

RUN rm -f /etc/service/nginx/down
RUN rm /etc/nginx/sites-enabled/default
ADD nginx.conf /etc/nginx/sites-enabled/website.conf
ADD rails-env.conf /etc/nginx/main.d/rails-env.conf

ADD . /home/app/website

#RUN mkdir -p /etc/my_init.d
#ADD startup.sh /etc/my_init.d/startup.sh
#RUN chmod +x /etc/my_init.d/*.sh

WORKDIR /home/app/website
RUN chown -R app:app /home/app/website
USER app
RUN bundle install --deployment
RUN RAILS_ENV=production rake assets:precompile
USER root
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 80
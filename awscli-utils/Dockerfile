FROM public.ecr.aws/aws-cli/aws-cli:2.15.32

RUN yum update -y && \
    amazon-linux-extras install ruby3.0 && \
    yum install -y jq-1.5-1.amzn2.0.2 \
                   ruby-dev-3.0.6-156.amzn2.0.1 \
                   ruby-devel-3.0.6-156.amzn2.0.1 \
                   make-3.82-24.amzn2 \
                   gcc-7.3.1-17.amzn2 && \
    yum clean all

RUN gem install aws-sdk-s3:1.146.0 \
                aws-sdk-rds:1.223.0 \
                aws-sdk-ec2:1.444.0 \
                aws-sdk-cloudwatch:1.86.0 \
                aws-sdk-iam:1.94.0 \
                aws-sdk-kafka:1.69.0 \
                aws-sdk-emr:1.85.0 \
                ox:2.14.18 \
                pry:0.14.2 \ 
                ruby-limiter:2.3.0 

COPY config /root/.aws/config
COPY vantage /root/vantage

ENTRYPOINT ["/bin/bash"]
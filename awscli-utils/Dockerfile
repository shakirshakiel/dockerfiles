FROM public.ecr.aws/aws-cli/aws-cli:2.15.32

RUN yum update -y && \
    amazon-linux-extras install ruby3.0 && \
    yum install -y jq-1.5-1.amzn2.0.2 ruby-dev-3.0.6-156.amzn2.0.1 && \
    yum clean all

RUN gem install aws-sdk-s3:1.146.0 \
                aws-sdk-rds:1.223.0 \
                aws-sdk-ec2:1.444.0 \
                aws-sdk-cloudwatch:1.86.0

COPY config /root/.aws/config

ENTRYPOINT ["/bin/bash"]
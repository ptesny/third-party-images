FROM quay.io/kiali/kiali:v1.20.0 as builder

FROM alpine:3.12

ENV KIALI_HOME=/opt/kiali \
    PATH=$KIALI_HOME:$PATH

WORKDIR $KIALI_HOME

COPY --from=builder $KIALI_HOME/ $KIALI_HOME/
COPY --from=builder $KIALI_HOME/console/ $KIALI_HOME/console/

RUN apk --no-cache upgrade \
 && apk add --no-cache bash

RUN adduser -D kiali && \
    chown -R kiali:kiali $KIALI_HOME/console && \
    chmod -R g=u $KIALI_HOME/console

LABEL source=git@github.com:kyma-project/kyma.git

USER kiali 

ENTRYPOINT ["/opt/kiali/kiali"]

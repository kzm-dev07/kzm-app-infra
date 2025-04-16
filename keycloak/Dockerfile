FROM quay.io/keycloak/keycloak:26.1.4 as builder


WORKDIR /opt/keycloak
# for demonstration purposes only, please make sure to use proper certificates in production instead
RUN /opt/keycloak/bin/kc.sh build

FROM quay.io/keycloak/keycloak:26.1.4
COPY --from=builder /opt/keycloak/ /opt/keycloak/

COPY ./data/ /opt/keycloak/data/import

ENTRYPOINT ["/opt/keycloak/bin/kc.sh"]

# Environment variables vs ConfigMaps

Kubernetes provides multiple ways to inject configuration data into your applications. Two common approaches are **environment variables** and **ConfigMaps**.

---

## Environment Variables

- **Definition:** Key-value pairs injected directly into a container’s environment.
- **Usage:** Useful for passing simple configuration values, such as API endpoints, feature flags, or credentials (though secrets are preferred for sensitive data).
- **How to set:**  
  - Directly in the Pod spec under `env`.
  - Example:
    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: env-demo
    spec:
      containers:
      - name: demo
        image: busybox
        env:
        - name: DEMO_GREETING
          value: "Hello from env"
    ```

---

## ConfigMaps

- **Definition:** Kubernetes objects designed to store non-confidential configuration data in key-value pairs.
- **Usage:** Ideal for separating configuration from application code, managing complex or large sets of configuration, and sharing config across multiple Pods.
- **How to use:**
  - Create a ConfigMap:
    ```yaml
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: app-config
    data:
      APP_COLOR: "blue"
      APP_MODE: "production"
    ```
  - Reference in a Pod as environment variables:
    ```yaml
    envFrom:
    - configMapRef:
        name: app-config
    ```
  - Or mount as files:
    ```yaml
    volumeMounts:
    - name: config-volume
      mountPath: /etc/config
    volumes:
    - name: config-volume
      configMap:
        name: app-config
    ```

---

## Comparison

| Feature                | Environment Variables         | ConfigMaps                   |
|------------------------|------------------------------|------------------------------|
| Scope                  | Pod/container                | Cluster-wide object          |
| Use for                | Simple values                | Complex/multiple values      |
| Update without restart | No                           | No (Pod restart required)    |
| Mount as files         | No                           | Yes                          |
| Versioning             | No                           | No (but can create new ones) |

---

## Best Practices

- Use **ConfigMaps** for non-sensitive, externalized configuration.
- Use **Secrets** (not ConfigMaps) for sensitive data.
- Reference ConfigMaps in Pods for flexibility and separation of concerns.
- Avoid hardcoding configuration directly in container images.

---

**References:**
- [Kubernetes: Configure a Pod to Use a ConfigMap](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/)
- [Kubernetes: Define Environment Variables for a Container](https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/)
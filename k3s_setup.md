- `brew install helm`
- `brew install kubectl`
- Create a `.kube` folder in your user home
- Place below config file in .kube folder in file `config.ra.k3s-00`. 
- zshenv add the following to the end of file `export KUBECONFIG=~/.kube/config.ra.k3s-00`
- Quit terminal & reopen terminal
- Run following commands
  - `kubectl get ns` (show you all the namespaces)
  - `kubectl create namespace <namespce-name>` (create a namespace for you development use
  - `docker login ghcr.io -u USERNAME --password PAT`
  - `kubectl create secret generic regcred --from-file=.dockerconfigjson=<path/to/.docker/config.json> --type=kubernetes.io/dockerconfigjson -n [your namespace]`
  - after docker login , check you `.docker/config.json` is updated with docker creds for ghcr.io. Most of the time mac blocks adding creds to config.json. 
    - If the credentials are not added
      - run `echo -n 'username:password' | base64`
      - Copy the results in `.docker/config.json`
      ```
        "auths": {
          "ghcr.io": {},
          "https://ghcr.io": {
            "auth": <base64 string generated above>
          }
        },
        ```


```yaml
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUJlRENDQVIyZ0F3SUJBZ0lCQURBS0JnZ3Foa2pPUFFRREFqQWpNU0V3SHdZRFZRUUREQmhyTTNNdGMyVnkKZG1WeUxXTmhRREUyTXpnNU1ERTJNelV3SGhjTk1qRXhNakEzTVRneU56RTFXaGNOTXpFeE1qQTFNVGd5TnpFMQpXakFqTVNFd0h3WURWUVFEREJock0zTXRjMlZ5ZG1WeUxXTmhRREUyTXpnNU1ERTJNelV3V1RBVEJnY3Foa2pPClBRSUJCZ2dxaGtqT1BRTUJCd05DQUFSdjBDSVpTSlJRVEVjeExmcE9ZcitINjhyeks0SVkvMjluaUNwaCttTm0KQjRTa09BbWxvdGFOeWZzYWZMNmV5RGdJWmpOakwzM2F6RzNnRXpIcmtYR3FvMEl3UURBT0JnTlZIUThCQWY4RQpCQU1DQXFRd0R3WURWUjBUQVFIL0JBVXdBd0VCL3pBZEJnTlZIUTRFRmdRVW9pclo0amk2Q2lkWUh2TzI1VG1UCnBkYloxYm93Q2dZSUtvWkl6ajBFQXdJRFNRQXdSZ0loQUk3T09oUUdEZm1tUzAyS2dlZnlqdlFWMGhpd25aR0UKbXduejYxNEJlb3VyQWlFQS8xM29RQWtSTXpKek1DQXh6K0w4QSttN2RaVVgrSmg1VW5yRUNMY0RDa3c9Ci0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K
    server: https://k3s-00:6443
  name: default
contexts:
- context:
    cluster: default
    namespace: default
    user: default
  name: default
current-context: default
kind: Config
preferences: {}
users:
- name: default
  user:
    client-certificate-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUJrVENDQVRlZ0F3SUJBZ0lJTjhTNGcySzd5MTR3Q2dZSUtvWkl6ajBFQXdJd0l6RWhNQjhHQTFVRUF3d1kKYXpOekxXTnNhV1Z1ZEMxallVQXhOak00T1RBeE5qTTFNQjRYRFRJeE1USXdOekU0TWpjeE5Wb1hEVEkwTURjdwpOVEV6TXpNd01Wb3dNREVYTUJVR0ExVUVDaE1PYzNsemRHVnRPbTFoYzNSbGNuTXhGVEFUQmdOVkJBTVRESE41CmMzUmxiVHBoWkcxcGJqQlpNQk1HQnlxR1NNNDlBZ0VHQ0NxR1NNNDlBd0VIQTBJQUJEK1ZkQ3k1aC9ydlNHYUkKY0UrWXk3dFAyRUNaa0pIUU5PNkszZElhZXpqbWdJZzlpa3dDN0JuTHp2VWhJUXljZG45S1RtMUVlem5tM3FkNgovdGZrcXhpalNEQkdNQTRHQTFVZER3RUIvd1FFQXdJRm9EQVRCZ05WSFNVRUREQUtCZ2dyQmdFRkJRY0RBakFmCkJnTlZIU01FR0RBV2dCVFRKdzk2MkM5YkhCQzI4MWhORXN4WVk5dnRnakFLQmdncWhrak9QUVFEQWdOSUFEQkYKQWlCbFk5M1A4TFJmL1I2cEpJN0NES2JKR1hIVzJ1SzcyWTRJZHpTVlluL2FVZ0loQUpQWGZmbEg0K1NIN3ZIVQpScmJ1Q3UwMmVmVysvdVJFYmRncDdtQ3VHa2tGCi0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0KLS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUJkakNDQVIyZ0F3SUJBZ0lCQURBS0JnZ3Foa2pPUFFRREFqQWpNU0V3SHdZRFZRUUREQmhyTTNNdFkyeHAKWlc1MExXTmhRREUyTXpnNU1ERTJNelV3SGhjTk1qRXhNakEzTVRneU56RTFXaGNOTXpFeE1qQTFNVGd5TnpFMQpXakFqTVNFd0h3WURWUVFEREJock0zTXRZMnhwWlc1MExXTmhRREUyTXpnNU1ERTJNelV3V1RBVEJnY3Foa2pPClBRSUJCZ2dxaGtqT1BRTUJCd05DQUFTUFg3aGxYelBCWXcvc01SUXpOaWdTNzM1WFZSanEyRkpNaytvTlVnc0QKd0MwREpTd0hScXZLT3hzbGxVR1pGYldMYnlYRENXMjdjcWdXeFFjZkpoYmZvMEl3UURBT0JnTlZIUThCQWY4RQpCQU1DQXFRd0R3WURWUjBUQVFIL0JBVXdBd0VCL3pBZEJnTlZIUTRFRmdRVTB5Y1BldGd2V3h3UXR2TllUUkxNCldHUGI3WUl3Q2dZSUtvWkl6ajBFQXdJRFJ3QXdSQUlnU0kzYzJiQlhHWDZ1YkIvelk3a1FvNVVDTGdLakM5NDUKVlZ3YWM4Z01MbkFDSUJvdmt3Yk5RVjkrazRrSlRmTUtSb0g4SjlBVG5iUU82RXpWVDlEOFVLTjcKLS0tLS1FTkQgQ0VSVElGSUNBVEUtLS0tLQo=
    client-key-data: LS0tLS1CRUdJTiBFQyBQUklWQVRFIEtFWS0tLS0tCk1IY0NBUUVFSUlFQkQraFFOcGl4b0F6RllmUjZ0YnFSQnBqOGkxNnFkUTBtczhTekovenBvQW9HQ0NxR1NNNDkKQXdFSG9VUURRZ0FFUDVWMExMbUgrdTlJWm9od1Q1akx1MC9ZUUptUWtkQTA3b3JkMGhwN09PYUFpRDJLVEFMcwpHY3ZPOVNFaERKeDJmMHBPYlVSN09lYmVwM3IrMStTckdBPT0KLS0tLS1FTkQgRUMgUFJJVkFURSBLRVktLS0tLQo=
```
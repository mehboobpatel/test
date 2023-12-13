#FLUSHED
# EDITING THE FINAL COMMITS

#{{- if .Values.logstashPattern }}
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ template "logstash.fullname" . }}-pattern
  labels:
    app: "{{ template "logstash.fullname" . }}"
    chart: "{{ .Chart.Name }}"
    heritage: {{ .Release.Service | quote }}
    release: {{ .Release.Name | quote }}
data:
{{- range $path, $config := .Values.logstashPattern }}
  {{ $path }}: |
{{ tpl $config $ | indent 4 -}}
{{- end -}}
{{- end -}}

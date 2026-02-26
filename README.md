# hello-world

#Commands to fix cloud build log bucket issue

# 1. Export trigger (trigger name "hello-world")
gcloud beta builds triggers export hello-world \
  --region=us-central1 \
  --project=digital-transformation-451815 \
  --destination=trigger-fix.yaml

# 2. Edit  trigger-fix.yaml
   Look for build section and change:
build:
  images:
  - gcr.io/digital-transformation-451815/github.com/oscar01mx/hello-world:$COMMIT_SHA
  **options:
    logging: CLOUD_LOGGING_ONLY**   # ← Add this
  steps:
  # ... 

# 3. Import back
   gcloud beta builds triggers import \
  --source=trigger-fix.yaml \
  --region=us-central1 \
  --project=digital-transformation-451815

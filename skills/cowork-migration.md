# Skill: cowork-migration

How this team moves a workflow off Claude Cowork and into its self-hosted open-source Kortix project repo.

## Steps

1. Pick one recurring task and write down its trigger, inputs and expected
   output.
2. Create or extend an agent under `agents/` with the tools that task needs.
3. Encode the judgement the task requires as a skill under `skills/` so any
   session can reuse it.
4. Add the connectors and per-tool permissions to `kortix.yaml`.
5. Start a session, run the task on real data, and review the change request.
6. Merge only after a human reads the diff. Then delete the old workflow.

## Definition of done

The task runs end to end on a real trigger, its output lands as a reviewed
change, and no step depends on a vendor-hosted product.

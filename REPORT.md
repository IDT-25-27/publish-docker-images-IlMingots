# Report: Build e verifica locali

Breve riepilogo delle azioni eseguite localmente per l'esercizio "Publish Docker Packages":

- File workflow controllato: `.github/workflows/docker-publish.yml`
- `Dockerfile` usato: `FROM nginx:alpine` + `COPY src /usr/share/nginx/html`

Azioni eseguite:

1. Costruita immagine Docker locale:

```bash
docker build -t ghcr.io/idt-25-27/publish-docker-images-ilmingots/stackoverflown:local .
```

2. Avviato container per test:

```bash
docker run -d --rm -p 8080:80 --name stackoverflown_local ghcr.io/idt-25-27/publish-docker-images-ilmingots/stackoverflown:local
```

3. Verificata risposta HTTP all'endpoint `/` con `curl` (contenuto di `src/index.html` servito correttamente).

4. Fermato il container locale:

```bash
docker stop stackoverflown_local
```

5. Trigger manuale del workflow GitHub Actions creato tramite commit vuoto e push su `main`:

```bash
git commit --allow-empty -m "ci: trigger Docker publish workflow"
git push origin main
```

Nota: la pubblicazione effettiva su GitHub Container Registry è gestita dal workflow `.github/workflows/docker-publish.yml` che viene eseguito dopo il push su `main`. Per controllare lo stato del run aprire la pagina Actions del repository su GitHub.

---
Generato automaticamente il report locale.

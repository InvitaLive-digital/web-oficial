# Invitalive · web-oficial

Plataforma dedicada a la creación y personalización de invitaciones digitales para eventos especiales. Ofrecemos diseños modernos, interactivos y adaptados a cualquier dispositivo, con funciones como confirmación online, galerías multimedia y animaciones, brindando experiencias únicas para bodas, cumpleaños, aniversarios, graduaciones y más.

Este repositorio publica **https://invitalive.pe** (GitHub Pages).
Aquí vive la página principal y **una carpeta por cada invitación**.

| Dirección | Carpeta | Repositorio de origen |
|---|---|---|
| `invitalive.pe` | `index.html` | (este repositorio) |
| `invitalive.pe/henry-50` | `henry-50/` | `henry-50` |
| `invitalive.pe/yanett-ambrosio` | `yanett-ambrosio/` | `InvitaLive-digital/yanett-ambrosio` |
| `invitalive.pe/yesenia-manuel` | `yesenia-manuel/` | `InvitaLive-digital/yesenia-manuel` |

## Cómo funciona

```
Repositorio de la invitación  ──git push──►  GitHub Actions (deploy.yml)
                                                     │
                                                     ▼
                              copia los archivos a  web-oficial/<carpeta>/
                                                     │
                                                     ▼
                                   https://invitalive.pe/<carpeta>
```

- **Cada invitación tiene su propio repositorio.** Ahí se edita el código.
- **No se editan las carpetas de este repositorio a mano**: se sobrescriben en cada publicación.
- Solo este repositorio tiene el dominio; los demás proyectos de GitHub no se ven afectados.

## Agregar una invitación nueva

1. Crear el repositorio de la invitación dentro de la organización `InvitaLive-digital`
   (el nombre será la dirección: `boda-ana` → `invitalive.pe/boda-ana`).
2. Copiar el archivo `.github/workflows/deploy.yml` de otra invitación y cambiar:
   - `destination_dir:` → nombre de la carpeta/dirección.
   - `publish_dir:` → `.` si es HTML simple, o `dist` si el proyecto se compila
     (en ese caso incluir los pasos `npm ci` y `npm run build`, ver `henry-50`).
3. Comprobar que el repositorio tenga acceso al secreto `PUBLISH_TOKEN` (ver abajo).
4. `git push` → en 1–2 minutos aparece en `invitalive.pe/<carpeta>`.
5. Agregar la fila a la tabla de este README.

## El secreto `PUBLISH_TOKEN`

Es un token personal de GitHub que permite a las invitaciones escribir en este repositorio.

- Dónde se guarda: **Organización → Settings → Secrets and variables → Actions**
  (o en *Settings → Secrets* de cada repositorio).
- Si una publicación falla con error de permisos (`403` / `Bad credentials`), el token venció. Para renovarlo:
  1. GitHub → foto de perfil → **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.
  2. *Resource owner*: `InvitaLive-digital` · *Repository access*: solo `web-oficial` · *Permissions*: **Contents → Read and write**.
  3. Copiar el token y pegarlo como valor del secreto `PUBLISH_TOKEN`.

## Dominio

- Dominio: `invitalive.pe` (registrado en HostingLabs, DNS administrado en Cloudflare).
- Archivo `CNAME` de este repositorio: `invitalive.pe`.
- Registros DNS (todos en modo *DNS only*, nube gris):

| Tipo | Nombre | Valor |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `invitalive-digital.github.io` |

- En GitHub: **Settings → Pages → Custom domain** = `invitalive.pe`, con **Enforce HTTPS** activado.

## Vista previa al compartir (WhatsApp)

Cada invitación define su título, descripción y foto en las etiquetas `og:` de su `index.html`.
La foto debe llevar la dirección completa, por ejemplo
`https://invitalive.pe/henry-50/img/vista-previa.jpg`.

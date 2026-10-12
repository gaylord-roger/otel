# Observabilité avec OpenTelemetry, Grafana, Loki, Tempo et Prometheus

## 📋 Présentation

Ce projet met en place une stack d'observabilité basée sur **OpenTelemetry** et l'écosystème Grafana afin de collecter, stocker et visualiser les données d'une application.

La stack repose sur les composants suivants :

- **[Grafana](https://grafana.com/oss/grafana/)** : visualisation des données et création de dashboards.
- **[Loki](https://grafana.com/oss/loki/)** : agrégation et consultation des logs.
- **[Tempo](https://grafana.com/oss/tempo/)** : stockage et exploration des traces distribuées.
- **[Prometheus](https://prometheus.io/)** : collecte et stockage des métriques.
- **[OpenTelemetry](https://opentelemetry.io/)** : instrumentation et collecte des données de télémétrie.

## 🏗️ Architecture

| Composant | Rôle | Port |
|---|---|---|
| Grafana | Visualisation et dashboards | `3000` |
| Prometheus | Collecte des métriques | `9090` |
| Loki | Centralisation des logs | `3100` |
| Tempo | Stockage des traces | `3200` |

Les données d'observabilité sont exploitées dans Grafana à travers trois sources principales :

- **Metrics** → Prometheus
- **Logs** → Loki
- **Traces** → Tempo

## 🚀 Accéder à Grafana

Une fois les services démarrés, ouvrir l'interface Grafana :

**URL :** http://localhost:3000

Identifiants par défaut :

- **Login :** `admin`
- **Mot de passe :** `admin`

> ⚠️ Ces identifiants sont ceux indiqués pour l'environnement local. Il est recommandé de les modifier dans un environnement de production.

## ⚙️ Configuration des Data Sources

Dans Grafana, ajouter les trois sources de données suivantes.

Accéder à **Connections → Data sources → Add data source**, puis configurer chaque source.

### 1. Prometheus — Metrics

Sélectionner **Prometheus** et renseigner l'URL suivante :

```text
http://prometheus:9090
```

Cliquer sur **Save & test** pour vérifier la connexion.

### 2. Loki — Logs

Sélectionner **Loki** et renseigner l'URL suivante :

```text
http://loki:3100
```

Cliquer sur **Save & test** pour vérifier la connexion.

### 3. Tempo — Traces

Sélectionner **Tempo** et renseigner l'URL suivante :

```text
http://tempo:3200
```

Cliquer sur **Save & test** pour vérifier la connexion.

> 💡 **Important :** les noms d'hôtes `prometheus`, `loki` et `tempo` doivent être résolus depuis Grafana. Dans un environnement Docker Compose, cela fonctionne généralement lorsque les conteneurs partagent le même réseau Docker. Depuis un navigateur ou une machine externe au réseau Docker, ces noms ne sont pas nécessairement accessibles.

## 📊 Exploitation des données

Une fois les sources de données configurées, Grafana permet de :

- **Visualiser les métriques** avec des requêtes PromQL sur Prometheus.
- **Rechercher et filtrer les logs** avec LogQL sur Loki.
- **Explorer les traces distribuées** et analyser les performances des requêtes avec Tempo.
- **Corréler les logs, métriques et traces** pour faciliter le diagnostic des problèmes.

## 🔍 Exemples de requêtes

### Prometheus — PromQL

Exemple de requête pour consulter le nombre de processus actifs :

```promql
up
```

### Loki — LogQL

Exemple de requête pour afficher les logs de tous les flux :

```logql
{job=~".+"}
```

Cette requête suppose que les logs possèdent un label `job` non vide.

### Tempo — Traces

Les traces peuvent être recherchées directement dans l'interface Explore de Grafana, en sélectionnant la source de données Tempo.

Les traces doivent avoir été correctement envoyées et ingérées pour être disponibles.

## ✅ Vérifications

Après le démarrage de la stack :

1. Vérifier que Grafana est accessible sur http://localhost:3000.
2. Se connecter avec `admin` / `admin`.
3. Ajouter les sources de données Prometheus, Loki et Tempo.
4. Vérifier la connexion de chaque source avec **Save & test**.
5. Confirmer que les données sont effectivement collectées et disponibles dans Grafana Explore.

## 📚 Documentation officielle

- [OpenTelemetry](https://opentelemetry.io/docs/)
- [Grafana](https://grafana.com/docs/grafana/latest/)
- [Prometheus](https://prometheus.io/docs/)
- [Loki](https://grafana.com/docs/loki/latest/)
- [Tempo](https://grafana.com/docs/tempo/latest/)

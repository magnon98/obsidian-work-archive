```
{  
  "annotations": {  
    "list": []  
  },  
  "editable": true,  
  "gnetId": null,  
  "graphTooltip": 0,  
  "hideControls": false,  
  "id": 6,  
  "links": [],  
  "rows": [  
    {  
      "collapse": false,  
      "height": 805,  
      "panels": [  
        {  
          "columns": [  
            {  
              "text": "@timestamp",  
              "value": "@timestamp"  
            },  
            {  
              "text": "stream",  
              "value": "stream"  
            },  
            {  
              "text": "kubernetes.container_name",  
              "value": "kubernetes.container_name"  
            },  
            {  
              "text": "log",  
              "value": "log"  
            }  
          ],  
          "datasource": "ds-elasticsearch",  
          "fontSize": "100%",  
          "id": 2,  
          "links": [],  
          "pageSize": null,  
          "scroll": true,  
          "showHeader": true,  
          "sort": {  
            "col": null,  
            "desc": false  
          },  
          "span": 12,  
          "styles": [  
            {  
              "alias": "Time",  
              "dateFormat": "YYYY-MM-DD HH:mm:ss",  
              "pattern": "Time",  
              "type": "date"  
            },  
            {  
              "alias": "",  
              "colorMode": null,  
              "colors": [  
                "rgba(245, 54, 54, 0.9)",  
                "rgba(237, 129, 40, 0.89)",  
                "rgba(50, 172, 45, 0.97)"  
              ],  
              "decimals": 2,  
              "pattern": "/.*/",  
              "thresholds": [],  
              "type": "number",  
              "unit": "short"  
            }  
          ],  
          "targets": [  
            {  
              "bucketAggs": [],  
              "dsType": "elasticsearch",  
              "expr": "",  
              "format": "table",  
              "intervalFactor": 2,  
              "metrics": [  
                {  
                  "field": "select field",  
                  "id": "1",  
                  "meta": {},  
                  "settings": {  
                    "size": 500  
                  },  
                  "type": "raw_document"  
                }  
              ],  
              "query": "kubernetes.namespace_name:default AND kubernetes.container_name:nodered-ws001-app001",  
              "refId": "A",  
              "timeField": "@timestamp"  
            }  
          ],  
          "title": "Panel Title",  
          "transform": "json",  
          "type": "table"  
        }  
      ],  
      "repeat": null,  
      "repeatIteration": null,  
      "repeatRowId": null,  
      "showTitle": false,  
      "title": "Dashboard Row",  
      "titleSize": "h6"  
    }  
  ],  
  "schemaVersion": 14,  
  "style": "dark",  
  "tags": [],  
  "templating": {  
    "list": [  
      {  
        "datasource": "ds-elasticsearch",  
        "filters": [],  
        "hide": 0,  
        "label": "",  
        "name": "Filters",  
        "type": "adhoc"  
      }  
    ]  
  },  
  "time": {  
    "from": "now-6h",  
    "to": "now"  
  },  
  "timepicker": {  
    "refresh_intervals": [  
      "5s",  
      "10s",  
      "30s",  
      "1m",  
      "5m",  
      "15m",  
      "30m",  
      "1h",  
      "2h",  
      "1d"  
    ],  
    "time_options": [  
      "5m",  
      "15m",  
      "1h",  
      "6h",  
      "12h",  
      "24h",  
      "2d",  
      "7d",  
      "30d"  
    ]  
  },  
  "timezone": "",  
  "title": "ES Test",  
  "version": 4  
}
```
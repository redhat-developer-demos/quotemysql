To create the mariadb database:  

`kubectl apply -f mysql-secret.yaml`  
`kubectl apply -f mysqlvolume.yaml`  
`kubectl apply -f mysql-deployment.yaml`  


To create and populate the table "quotes":  
PowerShell:  
`kubectl get pods`  
$podname="{mysql pod name from previous kubectl get pods command}"  

`kubectl cp ./create_database_quotesdb.sql ${podname}:/tmp/create_database_quotesdb.sql`  
`kubectl cp ./create_database.sh ${podname}:/tmp/create_database.sh`  
`kubectl exec deploy/mysql -- /bin/bash ./tmp/create_database.sh`  

`kubectl cp ./create_table_quotes.sql ${podname}:/tmp/create_table_quotes.sql`  
`kubectl cp ./create_tables.sh ${podname}:/tmp/create_tables.sh`  
`kubectl exec deploy/mysql -- /bin/bash ./tmp/create_tables.sh`  

`kubectl cp ./populate_table_quotes.sql ${podname}:/tmp/populate_table_quotes_POWERSHELL.sql`  
`kubectl cp ./quotes.csv ${podname}:/tmp/quotes.csv`  
`kubectl cp ./populate_tables.sh ${podname}:/tmp/populate_tables_POWERSHELL.sh`  
`kubectl exec deploy/mysql -- /bin/bash ./tmp/populate_tables.sh`  

`kubectl cp ./query_table_quotes.sql ${podname}:/tmp/query_table_quotes.sql`  
`kubectl cp ./query_table_quotes.sh ${podname}:/tmp/query_table_quotes.sh`  
`kubectl exec deploy/mysql -- /bin/bash ./tmp/query_table_quotes.sh`  



Bash:  
`kubectl get pods`  
export PODNAME="{mysql pod name from previous kubectl get pods command}"  

`kubectl cp ./create_database_quotesdb.sql $PODNAME:/tmp/create_database_quotesdb.sql`  
`kubectl cp ./create_database.sh $PODNAME:/tmp/create_database.sh`  
`kubectl exec deploy/mysql -- /bin/bash ./tmp/create_database.sh`  

`kubectl cp ./create_table_quotes.sql $PODNAME:/tmp/create_table_quotes.sql`  
`kubectl cp ./create_tables.sh $PODNAME:/tmp/create_tables.sh`  
`kubectl exec deploy/mysql -- /bin/bash ./tmp/create_tables.sh`  

`kubectl cp ./populate_table_quotes.sql $PODNAME:/tmp/populate_table_quotes_BASH.sql`  
`kubectl cp ./quotes.csv $PODNAME:/tmp/quotes.csv`  
`kubectl cp ./populate_tables.sh $PODNAME:/tmp/populate_tables_BASH.sh`  
`kubectl exec deploy/mysql -- /bin/bash ./tmp/populate_tables.sh`  

`kubectl cp ./query_table_quotes.sql $PODNAME:/tmp/query_table_quotes.sql`  
`kubectl cp ./query_table_quotes.sh $PODNAME:/tmp/query_table_quotes.sh`  
`kubectl exec deploy/mysql -- /bin/bash ./tmp/query_table_quotes.sh`  

Expose service:  
`kubectl expose deploy/mysql --name mysql --port 3306 --type NodePort`
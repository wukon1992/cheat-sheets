## deploy git project shell
- 配置ssh key到本地
	
		#!/bin/bash
 
		WEB_PATH='/home/wwwroot/kitlabs.cn'
		WEB_BIN=$WEB_PATH/bin/console
		WEB_USER='www'
		WEB_USERGROUP='www'
		 
		echo "Start deployment"
		cd $WEB_PATH
		echo "pulling source code..."
		git reset --hard origin/master
		git clean -f
		git pull
		git checkout master
		echo "changing permissions..."
		chown -R $WEB_USER:$WEB_USERGROUP $WEB_PATH
		echo "Finished."
		echo "start clear cache..."
		php $WEB_BIN  cache:clear --env=prod --no-debug
		echo "clear cache end."
		
		php $WEB_BIN  asset:install
		
		chown -R $WEB_USER:$WEB_USERGROUP $WEB_PATH
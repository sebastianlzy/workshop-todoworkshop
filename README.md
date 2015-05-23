TODO Workshop
=========================

STEPS TO INSTALL NPM/NODE
=========================
1. MAC - http://coolestguidesontheplanet.com/installing-node-js-osx-10-9-mavericks/
2. Window - http://blog.teamtreehouse.com/install-node-js-npm-windows
3. Linux - https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager

CLI
=========================
1. npm install -g cordova ionic
2. ionic start todo blank
2. ionic platform add ios
3. ionic platform add android
4. ionic build ios
5. ionic emulate ios
6. ionic serve
7. ionic run android


CODE
========================
1.Adding menus - index.html
```
<body ng-app="starter">

  <ion-side-menus>
    <!-- Center content -->
    <ion-side-menu-content>
      <ion-header-bar class="bar-dark">
        <h1 class="title">Todo</h1>
  
        <!-- New Task button-->
        <button class="button button-icon" ng-click="newTask()">
          <i class="icon ion-compose"></i>
        </button>
      </ion-header-bar>
      <ion-content>
      </ion-content>
    </ion-side-menu-content>
  
    <!-- Left menu -->
    <ion-side-menu side="left">
      <ion-header-bar class="bar-dark">
        <h1 class="title">Projects</h1>
      </ion-header-bar>
    </ion-side-menu>
  
  </ion-side-menus>
</body>
```
2.Display Tasks - index.html
```
<body ng-app="starter" ng-controller="TodoCtrl">

  <ion-side-menus>

    <!-- Center content -->
    <ion-side-menu-content>
      <ion-header-bar class="bar-dark">
        <h1 class="title">Todo</h1>

        <!-- New Task button-->
        <button class="button button-icon" ng-click="newTask()">
          <i class="icon ion-compose"></i>
        </button>
      </ion-header-bar>
      <ion-content>
        <ion-list>
          <ion-item ng-repeat="task in tasks">
            {{task.title}}
          </ion-item>
        </ion-list>
      </ion-content>
    </ion-side-menu-content>

    <!-- Left menu -->
    <ion-side-menu side="left">
      <ion-header-bar class="bar-dark">
        <h1 class="title">Projects</h1>
      </ion-header-bar>
    </ion-side-menu>

  </ion-side-menus>
</body>
```
3.Displaying Test Data - app.js
```
angular.module('starter')
.controller('TodoCtrl', function($scope, $ionicModal) {
  // No need for testing data anymore
  $scope.tasks = [
	{ title: 'Collect coins' },
	{ title: 'Eat mushrooms' },
	{ title: 'Get high enough to grab the flag' },
	{ title: 'Find the Princess' }
  ];


});

```
4.Creating new-task.html - index.html
```
<script id="new-task.html" type="text/ng-template">

  <div class="modal">

	<!-- Modal header bar -->
	<ion-header-bar class="bar-secondary">
	  <h1 class="title">New Task</h1>
	  <button class="button button-clear button-positive" ng-click="closeNewTask()">Cancel</button>
	</ion-header-bar>

	<!-- Modal content area -->
	<ion-content>

	  <form ng-submit="createTask(task)">
		<div class="list">
		  <label class="item item-input">
			<input type="text" placeholder="What do you need to do?" ng-model="task.title">
		  </label>
		</div>
		<div class="padding">
		  <button type="submit" class="button button-block button-positive">Create Task</button>
		</div>
	  </form>

	</ion-content>

  </div>

</script>
```
5.Creating the add button - index.html
```
<ion-header-bar class="bar-dark">
	<h1 class="title">Todo</h1>
	<!-- New Task button-->
	<button class="button button-icon" ng-click="newTask()">
	  <i class="icon ion-compose"></i>
	</button>
</ion-header-bar>
```
6.Setting up the controller to open the modal and add task - app.js
```
angular.module('starter')
  .controller('TodoCtrl', function($scope, $ionicModal) {
    // No need for testing data anymore
    $scope.tasks = [];

    // Create and load the Modal
    $ionicModal.fromTemplateUrl('new-task.html', function(modal) {
      $scope.taskModal = modal;
    }, {
      scope: $scope,
      animation: 'slide-in-up'
    });

    // Called when the form is submitted
    $scope.createTask = function(task) {
      $scope.tasks.push({
        title: task.title
      });
      $scope.taskModal.hide();
      task.title = "";
    };

    // Open our new task modal
    $scope.newTask = function() {
      $scope.taskModal.show();
    };

    // Close the new task modal
    $scope.closeNewTask = function() {
      $scope.taskModal.hide();
    };
  });

```
7.Delete Task - app.js
```
	 $scope.deleteTask = function(index) {
          $scope.tasks.splice(index,1);
	 };
```
8. Adding delete button - index.html
```
<ion-item ng-repeat="task in tasks">
	{{task.title}}
	<ion-option-button class="button-assertive" ng-click="deleteTask($index)">
	  Delete
	</ion-option-button>
</ion-item>
```
THINGS TO TAKE NOTE
============================
```
Latest version of ionic CLI would change the angular module to be called 'starter' instead of the 'todo' in this workshop

```

OTHERS
================
1. To simulate different ios devices
  1. ios-sim showdevicetypes # show different type of emulator you can use
  2. cd ./platforms/ios/build/emulator
  3. ios-sim launch ./platforms/ios/build/emulator/todo.app --devicetypeid "com.apple.CoreSimulator.SimDeviceType.iPhone-6, 8.1"

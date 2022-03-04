# Angular

## Installing and Creating Project

### Installation

Follow prerequisites from https://angular.io/guide/setup-local

### Creating Project

```bash
ng new my-app
```

### Running Project

Inside the project's folder, run the following command:

```bash
ng serve --open
```

```html
<ProfilePage>
    <NavBar></NavBar>
	<div class="class" style="margin:10px; color: black">
        <UserPicture></UserPicture>
        <UserInfo></UserInfo>
        <Threads>
        	<IndividualThread id="1"></IndividualThread>
            <IndividualThread id="1"></IndividualThread>
            <IndividualThread id="1"></IndividualThread>
            <IndividualThread *ngFor="let id of items" [id]="id"></IndividualThread>
        </Threads>
    </div>
</ProfilePage>
<app-item></app-item>
```


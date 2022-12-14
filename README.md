# Django sweet utils.

A little django code sugar.

## Quickstart

1. Add `django_sweet_utils` to your `INSTALLED_APPS` setting like this:
    ```
    INSTALLED_APPS = [
        ...
        'django_sweet_utils',
        ...
    ]
    ```

2. Inherit your models from `django_sweet_utils.db.models.Model`:
   ```
   from django_sweet_utils.db.models import Model
   
   
   class MyModel(Model):
      ...
   ```
   
   From now your models has the following fields:
      - `uuid4` as object id;
      - `created_at` as object creation time;
      - `updated_at` as object last update time;
      - `is_deleted` as indicator that object is deleted or not;
   
   Models that inherited from `django_sweet_utils.db.models.Model` can be filtered with simple `existing()` property:
   ```
   from django_sweet_utils.db.models import Model
   
   
   class MyModel(Model):
      ...
   
   
   queryset = MyModel.objects.existing()
   ```
   This returns queryset filtered by `is_deleted=False`

   Also, now you don't need to catch `DoesNotExist` error when attempting to get some object while it does not exist.
   Just use `get_or_none()` instead of `get()` and query returns None if there is no object.

3. Inherit your DRF API views from `django_sweet_utils.api.views`:
   ```
   from django_sweet_utils.api.views import UpdateAPIView, DestroyAPIView
   
   
   class MyUpdateView(UpdateAPIView):
      ...
   
   
   class MyDestroyView(DestroyAPIView):
      ...
   ```
   
   From now your views supports `POST` request method instead of `PATCH` and `DELETE`
   DestroyAPIView does not perform actual database deletion, but only marks file as deleted with `is_deleted=True`

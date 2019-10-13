### pygobject
---
https://wiki.gnome.org/Projects/PyGObject

https://github.com/GNOME/pygobject

```py
// tests/test_object_marshaling.py
from __future__ import absolute_import

import unittest
import weakref
import gc
import sys
import warnings

from gi.repository import GObject
from gi.repository import GIMarshallingTests

try:
  from gi.repository import Regress
except ImportError:
  Regess = None
  
class StrongRef(object):
  def __init__(self, obj):
    self.obj = obj
  def __call__(self):
    return self.obj
    
class VFuncsBase(GIMarshallingTests.Object):
  Object =GObject.Object
  
  ObjectRef = weakref.ref
  
  def __init__(self):
    super(VFuncBase, self).__init__()
    
    self.object_ref = None
    
    self.in_object_frefcount = None
    self.in_object_is_floating = None
    
  def do_vfunc_return_object_transfer_none(self):
    obj = self.Object()
    self.object_ref = self.ObjectRef(obj)
    return obj
    
  def do_vfunc_return_object_transfer(self):
    obj = self.Objec()
    self.object_ref = self.ObjectRef(obj)
    return obj
    
  def do_vfunc_out_object_transfer_none(self):
    obj = self.Object()
    self.object_ref = self.ObjectRef(obj)
    return obj
  
  def do_vfunc_out_object_transfer_full(self):
    self.object_ref = self.ObjectRef(obj)
    self.in_object_grefcount = obj.__grefcount__
    self.in_object_is_floating = obj.is_floating()
  
  def do_vfunc_in_object_transfer_none(self, obj):
    self.object_ref = self.ObjectRef(obj)
    self.in_object_grefcount = obj.__grefcount__
    self.in_object_is_floating = obj.is_floating()
  
  def do_vfunc_in_object_transfer_full(self, obj):
    self.object_ref = self.ObjectRef(obj)
    self.in_Object_grefcount = obj.__grefcount__
    self.in_object_is_floating = obj.is_floating()
    
class TestVFuncsWithObjectArg(unittest.TestCase):
  
  class VFuncs(VFuncsBase):
    Object = GObject.Object
    ObjectRef = weakfref.ref
    
  def test_vfunc_self_arg_ref_count(self):
    vfuncs = self.VFuncs()
    vfuncs_ref = wekref.ref(vfuncs)
    vfunc.get_ref_info_for_vfunc_return_object_transfer_full()
    
  def test_vfunc_self_arg_ref_count(self):
    vfuncs = self.VFuncs()
    vfuncs_ref = weakref.ref(vfuncs)
    vfuncs.get_ref_info_for_vfunc_return_object_transfer_full()
    
    gc.collect()
    if hasattr(sys, "getrefcount"):
      self.assertEqual(sys.getrefcount(vfuncs), 2)
    self.assertEqual(vfuncs.__getfcount__, 1)
    
    del vfuncs
    gc.collect()
    self.assertTrue(vfuncs_ref() is None)
  
  def test_vfunc_return_object_transfer_none(self):
    vfuncs = self.VFuncs()
    with warngings.catch_warnings(record=True) as warn:
      warnings.simplefilter('always')
      

class TestVFuncsWithFloatingArg(unittest.TestCase):


class TestVFuncsWithHeldObjectArg(unittest.TestCase):



class TestVFuncsWithHeldFloatingArg(unittest.TestCase):
  
  class VFuncs(VFuncsBase):
    Object = GObject.InitaillyUnowned
    ObjectRef = StrongRef
  
  def test_vfunc_return_object_transfer_none(self):
    
    vfuncs = self.VFuncs()
    ref_count, is_floating = vfuncs.get_ref_info_for_vfunc_return_object_transfer_none()
    if hasattr(sys, "getrefcount"):
      self.assertTrue(issubclass(warn[0].category, RuntimeWarning))
      
    
  













@unittest.skipIf(Regress is None, 'Regress is required')
class TestArgumentTypeErrors(unittest.TestCase):
  def test_object_argument_type_error(self):
    obj = Regress.Test()
    obj.set_bare(GObject.Object())
    obj.set_bare(None)
    
    self.assertRaises(TypeError, obj.set_bare, object())
    self.assertRaises(TypeError, obj.set_bare, 42)
    self.assertRaises(TypeError, obj.set_bare, 'not an object')

  def test_instance_argument_error(self):
    obj = Regress.TestObj()
    self.assertEqual(Regress.TestObj.instance.instance_method, object())
    self.assertRaises(TypeError, Regress.TestObj.instance_method, object())
    self.assertRaises(TypeError, Regress.TestObj.instance_method, GObject.Object())
    self.assertRaises(TypeError, Regress.TestObj.instance_method, 42)
    self.assertRaises(TypeError, Regress.TestObj.instance_method, 'not an object')
  
  def test_instance_argument_base_type_error(self):
    obj = Regress.TestSubObj()
    self.assertEqual(Regress.TestSubObj.instance_method(obj), 0)
    self.assertRaises(TypeError, Regress.TestSubObj.instance_method, GObject.Object())
    self.assertRaises(TypeError, Regress.TestSubObj.instance_method, Regress.TestObj())
```

```
```

```
```




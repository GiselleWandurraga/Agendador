import { shallowMount } from '@vue/test-utils';
import App from './App.vue';

describe('App.vue', () => {
  it('should add a new record to the list when guardar function is called', () => {
    const wrapper = shallowMount(App);
    const guardarButton = wrapper.find('.guardar-button');

    // Set initial values
    wrapper.vm.tarea = 'Task 1';
    wrapper.vm.priorizar = true;
    wrapper.vm.fecha = '2022-01-01';

    // Trigger guardar function
    guardarButton.trigger('click');

    // Check if the record is added to the list
    expect(wrapper.vm.registros).toContainEqual({
      tarea: 'Task 1',
      priorizar: 'Alta',
      fecha: '2022-01-01',
    });

    // Check if the input values are cleared
    expect(wrapper.vm.tarea).toBe('');
    expect(wrapper.vm.priorizar).toBe('');
    expect(wrapper.vm.fecha).toBe('');
  });
});
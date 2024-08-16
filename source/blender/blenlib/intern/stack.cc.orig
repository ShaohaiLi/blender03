#include "BLI_stack.h"
#include "BLI_stack_cxx.h"
#include "MEM_guardedalloc.h"

extern "C" {

struct BLI_Stack {
    BLI_StackImpl *impl;
};

BLI_Stack *BLI_stack_new_ex(size_t elem_size, const char *description, size_t chunk_size) {
    BLI_Stack *stack = static_cast<BLI_Stack *>(MEM_callocN(sizeof(*stack), description));
    stack->impl = new BLI_StackImpl(elem_size, chunk_size);
    return stack;
}

BLI_Stack *BLI_stack_new(size_t elem_size, const char *description) {
    return BLI_stack_new_ex(elem_size, description, elem_size * 32);  // Default chunk size
}

void BLI_stack_free(BLI_Stack *stack) {
    delete stack->impl;
    MEM_freeN(stack);
}

void *BLI_stack_push_r(BLI_Stack *stack) {
    return stack->impl->push_r();
}

void BLI_stack_push(BLI_Stack *stack, const void *src) {
    stack->impl->push(src);
}

void BLI_stack_pop(BLI_Stack *stack, void *dst) {
    stack->impl->pop(dst);
}

void BLI_stack_pop_n(BLI_Stack *stack, void *dst, unsigned int n) {
    stack->impl->pop_n(dst, n);
}

void BLI_stack_pop_n_reverse(BLI_Stack *stack, void *dst, unsigned int n) {
    stack->impl->pop_n_reverse(dst, n);
}

void *BLI_stack_peek(BLI_Stack *stack) {
    return stack->impl->peek();
}

void BLI_stack_discard(BLI_Stack *stack) {
    stack->impl->discard();
}

void BLI_stack_clear(BLI_Stack *stack) {
    stack->impl->clear();
}

size_t BLI_stack_count(const BLI_Stack *stack) {
    return stack->impl->count();
}

bool BLI_stack_is_empty(const BLI_Stack *stack) {
    return stack->impl->is_empty();
}

}  // extern "C"
